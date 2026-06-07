---
date: '2026-06-07T12:00:00+08:00'
title: '自建分布式 MCP 记忆服务：让 AI  Agent 跨会话、跨机器共享记忆'
tags: ["MCP", "AI", "教程", "部署", "OpenCode"]
cover:
  image: "/images/mcp-memory-cover.svg"
  alt: "MCP Memory Service 架构图"
  caption: "Nginx + Let's Encrypt + MCP 记忆服务 + OpenCode"
---

## 背景

AI Agent（比如 Cursor、Windsurf、OpenCode、Claude Code 等）在单个会话内表现很好，但跨会话后就"失忆"了。每次新会话都要重新告诉它你的偏好、项目上下文、历史决策记录。

更麻烦的是，如果在多台机器上工作（台式机 + 笔记本），每台机器上的 Agent 都是完全独立的——这台知道的事，那台完全不知道。

市面上有几种解决方案：

| 方案 | 类型 | 自部署 | OAuth | 远程 MCP |
|------|------|--------|-------|---------|
| **OpenMemory** | 云服务 | ❌ | ❌ | ✅ |
| **shared-context-mcp** | 本地文件 | ❌ | ❌ | ❌ |
| **Continuum** | VSCode 插件 | ❌ | ❌ | ❌ |
| **mcp-memory-service** | 自部署服务 | ✅ | ✅ | ✅ |

我选择了 **mcp-memory-service**——一个开源、自托管的语义记忆服务。用下来最大的感受：这才是 Agent 应有的工作方式。

---

## 架构

```
                    ┌─────────────┐
                    │ OpenCode    │
                    │ (本地终端)   │
                    └──────┬──────┘
                           │ MCP Streamable HTTP
                           ▼
               ┌─────────────────────┐
               │  memory.bishengzhihui.cn  │
               │  (HTTPS)            │
               │  Let's Encrypt SSL   │
               └──────────┬──────────┘
                          │
                    ┌─────┴─────┐
                    │  Nginx   │
                    │  反代     │
                    └─────┬─────┘
                          │
               ┌──────────┴──────────┐
               │  127.0.0.1:8001     │
               │  mcp-memory-service  │
               │  (FastAPI + Uvicorn) │
               │                     │
               │  / → Web Dashboard  │
               │  /mcp → MCP 端点    │
               │  /events → SSE      │
               └─────────────────────┘
```

### 关键端口

| 端口 | 绑定地址 | 用途 |
|------|---------|------|
| 8001 | 127.0.0.1 | HTTP REST API + Web 管理面板 + MCP 端点 |
| 8765 | 127.0.0.1 | MCP SSE 传输（备选） |
| 80/443 | 0.0.0.0 | Nginx 监听，带 SSL |

### 数据流

```
用户发消息 → OpenCode → MCP 协议 → memory.bishengzhihui.cn
                                 → Nginx (SSL 终止)
                                 → mcp-memory-service
                                 → SQLite-vec (本地向量数据库)
                                 → embedding 模型生成向量
                                 → 语义搜索 + 记忆存储
```

---

## 功能特性

mcp-memory-service 是一个成熟的产品（v10.74.1），功能相当完整：

| 功能 | 说明 |
|------|------|
| **语义记忆** | 基于 embedding 的语义搜索，非简单关键词匹配 |
| **自动合并** | 相关记忆自动合并，避免碎片化 |
| **标签系统** | 支持标签分类和筛选 |
| **会话隔离** | 通过 `conversation_id` 区分不同会话 |
| **MCP 协议** | 原生支持 Model Context Protocol |
| **OAuth 2.1** | 支持 Google/GitHub 等第三方登录 |
| **API Key 认证** | `Authorization: Bearer <key>` |
| **知识图谱** | 记忆之间的关联图谱（可选） |
| **文档导入** | 支持 PDF、Markdown 等文件导入 |
| **Web 面板** | 浏览器直接管理记忆 |
| **多种存储** | SQLite-vec 本地 / Cloudflare D1 云同步 / Hybrid 混合 |
| **mDNS 发现** | 局域网自动发现 |

### MCP 工具

部署后，OpenCode 能直接调用以下工具：

| 工具 | 功能 |
|------|------|
| `memory_store` | 存储新记忆 |
| `memory_read` | 读取指定记忆 |
| `memory_search` | 语义搜索记忆 |
| `memory_update` | 更新已有记忆 |
| `memory_delete` | 删除记忆 |
| `memory_list_tags` | 列出所有标签 |
| `memory_stats` | 记忆统计信息 |

---

## 部署方案

### 服务器要求

| 项目 | 最低要求 | 推荐 |
|------|---------|------|
| **CPU** | 1 核 | 2 核+ |
| **内存** | 1GB | 2GB+ |
| **磁盘** | 5GB | 10GB+（含 embedding 模型） |
| **Python** | 3.10+ | 3.11+ |
| **系统** | Linux | Ubuntu 22.04 / Debian 12 / Alibaba Cloud Linux 3 |
| **域名** | 需一个域名和 SSL | 已有 Let's Encrypt |

### 部署步骤

#### 1. 安装依赖

```bash
# 安装 Python 3.11
dnf install -y python3.11 python3.11-pip python3.11-devel

# 创建虚拟环境
python3.11 -m venv /opt/mcp-memory-service/venv
source /opt/mcp-memory-service/venv/bin/activate
```

#### 2. 安装项目

```bash
# 克隆或上传源码后
cd /opt/mcp-memory-service/app
pip install -e .

# 或通过 pip 直接安装
pip install mcp-memory-service
```

#### 3. 配置 systemd 服务

```ini
[Unit]
Description=MCP Memory Service
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/opt/mcp-memory-service
Environment=HF_ENDPOINT=https://hf-mirror.com
Environment=MCP_HTTP_HOST=127.0.0.1
Environment=MCP_HTTP_PORT=8001
Environment=MCP_SSE_HOST=127.0.0.1
Environment=MCP_SSE_PORT=8765
Environment=MCP_ALLOW_ANONYMOUS_ACCESS=true
Environment=MCP_MEMORY_SQLITE_PATH=/opt/mcp-memory-service/data/memory.db
ExecStart=/opt/mcp-memory-service/venv/bin/memory server --http --http-host 127.0.0.1 --http-port 8001 --sse-port 8765
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

```bash
systemctl daemon-reload
systemctl enable mcp-memory
systemctl start mcp-memory
```

#### 4. 配置 Nginx 反代

```nginx
server {
    listen 80;
    server_name memory.yourdomain.com;

    location /.well-known/acme-challenge/ {
        root /var/www/html;
    }

    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    server_name memory.yourdomain.com;

    ssl_certificate     /etc/letsencrypt/live/memory.yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/memory.yourdomain.com/privkey.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;

    client_max_body_size 100M;

    location / {
        proxy_pass http://127.0.0.1:8001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    location /mcp {
        proxy_pass http://127.0.0.1:8001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    location /events {
        proxy_pass http://127.0.0.1:8001;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_buffering off;
        proxy_cache off;
        proxy_read_timeout 86400s;
    }
}
```

#### 5. 获取 SSL 证书

```bash
certbot certonly --webroot -w /var/www/html -d memory.yourdomain.com
```

> **注意**：国内服务器无法直接访问 huggingface.co 下载 embedding 模型，需要配置镜像源：
> ```bash
> export HF_ENDPOINT=https://hf-mirror.com
> ```
> 或在 systemd 服务中加入 `Environment=HF_ENDPOINT=https://hf-mirror.com`

---

## 在 OpenCode 中配置 MCP 连接

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "memory-service": {
      "type": "remote",
      "url": "https://memory.bishengzhihui.cn/mcp",
      "enabled": true
    }
  }
}
```

### 认证模式

| 模式 | 配置 | 适用场景 |
|------|------|---------|
| **匿名** | `MCP_ALLOW_ANONYMOUS_ACCESS=true` | 内网测试 |
| **API Key** | `MCP_API_KEY=your-secret-key` | 个人生产环境 |
| **OAuth 2.1** | `MCP_OAUTH_ENABLED=true` | 多用户场景 |

API Key 模式下的 OpenCode 配置：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "memory-service": {
      "type": "remote",
      "url": "https://memory.bishengzhihui.cn/mcp",
      "headers": {
        "Authorization": "Bearer {env:MCP_API_KEY}"
      }
    }
  }
}
```

---

## 验证部署是否正常

部署完成后，可以用 curl 验证 MCP 端点是否正常：

```bash
# 初始化
curl -s -X POST https://memory.yourdomain.com/mcp \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{"protocolVersion":"2024-11-05","capabilities":{},"clientInfo":{"name":"test","version":"1.0"}}}'

# 列出工具
curl -s -X POST https://memory.yourdomain.com/mcp \
  -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/list","params":{}}'
```

预期结果：

```json
// initialize 返回
{"jsonrpc":"2.0","id":1,"result":{"protocolVersion":"2024-11-05","capabilities":{"tools":{}},"serverInfo":{"name":"mcp-memory-service","version":"10.74.1"}}}

// tools/list 返回
{"jsonrpc":"2.0","id":2,"result":{"tools":[
  {"name":"memory_store","description":"Store new information..."},
  {"name":"memory_search","description":"Semantic search..."},
  {"name":"memory_read","description":"Read memory by ID..."}
]}}
```

---

## 日常使用

### 存记忆

在 OpenCode 中直接使用：

```
/agent memory-store "用户偏好暗色主题，编辑器字体设置为 JetBrains Mono 14px"
```

### 搜记忆

```
/agent memory-search "用户对主题的偏好"
```

### 跨机器共享

在台式机上存：

```
memory_store content="项目 A 的 API 设计采用 RESTful 风格，认证方式为 JWT"
```

在笔记本上问：

```
memory_search query="项目 A 的 API 认证方式"
```

两台设备共享同一个记忆服务，Agent 能直接查到。

### Web 管理面板

浏览器打开 `https://memory.yourdomain.com` 即可看到管理面板，支持：
- 查看/搜索/编辑所有记忆
- 标签管理
- 文档导入
- 系统配置
- 统计信息

---

## 进阶配置

### 存储后端选择

| 后端 | 适用场景 | 优势 |
|------|---------|------|
| **SQLite-vec**（默认） | 单机部署 | 零依赖，最简配置 |
| **Cloudflare D1 + Vectorize** | 多节点共享 | 云端同步，全球可用 |
| **Hybrid** | 复杂场景 | 本地 + 云端混合 |
| **Milvus** | 大规模生产 | 分布式向量数据库 |

### 环境变量参考

| 变量 | 默认值 | 说明 |
|------|--------|------|
| `MCP_HTTP_PORT` | 8000 | HTTP 服务端口 |
| `MCP_HTTP_HOST` | 127.0.0.1 | HTTP 绑定地址 |
| `MCP_SSE_PORT` | 8765 | SSE 传输端口 |
| `MCP_ALLOW_ANONYMOUS_ACCESS` | false | 允许匿名访问 |
| `MCP_API_KEY` | (无) | API Key 认证 |
| `MCP_OAUTH_ENABLED` | false | 启用 OAuth 2.1 |
| `MCP_MEMORY_SQLITE_PATH` | ./data/memory.db | 数据库路径 |
| `MCP_MEMORY_STORAGE_BACKEND` | sqlite_vec | 存储后端 |
| `HF_ENDPOINT` | https://huggingface.co | 模型下载镜像 |

---

## 注意事项

### 1. 国内服务器需配置 HF 镜像

国内服务器无法直连 huggingface.co 下载 embedding 模型，必须设置：

```bash
export HF_ENDPOINT=https://hf-mirror.com
```

### 2. 首次启动需要下载模型

首次启动会自动下载 `all-MiniLM-L6-v2` 模型（约 80MB），耗时约 1-3 分钟。服务会等模型下载完成后才开始监听端口。

### 3. 端口冲突

如果 8000 端口已被占用（比如已有其他服务），通过 `--http-port` 指定其他端口。

### 4. SSL 证书续期

Let's Encrypt 证书 90 天有效期，建议配置自动续期：

```bash
# certbot 默认已配置 systemd timer
systemctl list-timers | grep certbot
```

### 5. 内存占用

embedding 模型加载后约占用 500MB-1GB 内存，如果服务器内存紧张可以考虑用 ONNX Runtime 替代 PyTorch：

```bash
pip install onnxruntime
```

---

## 总结

| 维度 | 评价 |
|------|------|
| **易用性** | ⭐⭐⭐⭐⭐ 配置完 OpenCode 自动发现，无需手动调用 |
| **可靠性** | ⭐⭐⭐⭐ SQLite-vec 存储稳定，systemd 自动重启 |
| **安全性** | ⭐⭐⭐⭐⭐ 支持 API Key / OAuth / HTTPS |
| **跨平台** | ⭐⭐⭐⭐⭐ 任何支持 MCP 的客户端都能用 |
| **成本** | ⭐⭐⭐⭐⭐ 自部署，零月费（已有服务器） |

mcp-memory-service 的成熟度超出预期，v10.74.1 版本已经是一个非常完整的语义记忆平台。如果你也在用 AI Agent 编程，强烈建议部署一套——它在多会话、多机器场景下的体验提升是质变的。

---

> **本文由 LLM 辅助生成**。技术细节经实测验证。
