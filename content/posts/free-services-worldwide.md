---
date: '2026-05-20T01:00:00+08:00'
title: '2026 全球免费云服务/工具大合集（200+ 个资源）'
tags: ["资源", "免费", "教程", "汇总"]
cover:
  image: "/images/free-worldwide-cover.svg"
  alt: "全球免费资源分类图"
  caption: "覆盖计算、存储、数据库、AI 等各大品类"
---

## 前言

2026 年，全球主流云平台和 SaaS 厂商的免费计划已经卷到了新高度。从 4 核 ARM 服务器永免到无限带宽 CDN，从 25GB 数据库到百万级免费 API 调用——个人开发者不花一分钱就能撑起一个生产级应用。

本文系统整理了 **18 大类、200+ 个免费资源**，每个都标注免费额度、适用场景、注意事项。文末有 **推荐组合**，直接抄作业即可。

---

## 一、云计算（IaaS）

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Oracle Cloud Always Free** | 4 核 ARM + 24GB RAM + 200GB 存储 **永免**；2 个 AMD 微实例 | 个人 VPS、VPN、博客、Web 服务 | 注册需信用卡验证；ARM 实例性能极好但偶尔被回收空闲资源 |
| **AWS Free Tier** | 12 个月：t2.micro / t3.micro (750h/月)；5GB S3；25GB DynamoDB | 入门云计算、学习 AWS 生态 | 12 个月后自动收费，务必设账单告警 |
| **Google Cloud Always Free** | 1 个 f1-micro (0.6GB RAM) + 30GB HDD，每月 2M Cloud Functions | 轻量后端、学习 GCP | 带宽限制严格；f1-micro 性能一般 |
| **Azure Free** | 12 个月：1 个 B1s (1GB RAM)；100GB 存储 | 微软生态集成、.NET 项目 | 免费期后 $13.99/月费用，注意关闭资源 |
| **IBM Cloud Lite** | 256MB RAM 的 VM + Cloud Foundry 应用托管 | 轻量实验、学习 IBM 平台 | 额度非常有限，生产用途不推荐 |
| **Alibaba Cloud Free Trial** | 1 个月试用：1 核 2GB ECS；部分服务 3-6 个月 | 阿里云生态入门 | 试用期短，到期成本高 |
| **Tencent Cloud Free** | 1 个月：1 核 2GB CVM；6 个月 50GB COS | 腾讯云入门 | 短期试用为主 |
| **Huawei Cloud Free** | 6 个月：1 核 1GB ECS + 40GB 硬盘 | 华为云生态学习 | 仅新用户，时长有限 |
| **Vultr** | 新用户 $300 额度（30 天） | 短期高规格测试 | 额度过期即止 |
| **Linode (Akamai)** | 新用户 $100 额度（60 天） | 开发者测试 | 需信用卡，超时收费 |

> **Oracle Cloud Always Free** 是 IaaS 层的"神级"存在——4 核 ARM + 24GB RAM 永久免费，跑 Docker/数据库/VPN 都够用。但注册成功率偏低且资源可能被收回，建议部署重要服务前做好备份。

---

## 二、前端托管

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Vercel** | 100GB 带宽/月 + 不限构建次数 | Next.js / 前端项目 | 商业项目需加品牌标识；带宽超限可能停用 |
| **Netlify** | 100GB 带宽/月 + 300 构建分钟/月 | 静态站 + Functions + 表单 | Function 调用量限制 125k/月 |
| **Cloudflare Pages** | **无限带宽** + 500 次构建/月 | 静态站 + Pages Functions | 构建并发限制 1 个；文件数建议 <20k |
| **GitHub Pages** | 无限带宽（1GB 限制） + 10 次构建/小时 | 个人/项目主页 | 仅限静态站；仓库 ≤1GB |
| **Render** | 750 小时/月静态站 + 100GB 带宽 | 静态站 + 服务端渲染 | 实例 15 分钟无访问会休眠 |
| **Surge** | 无限带宽 + 20 次部署 | 纯静态站快速部署 | CLI 操作，无图形管理界面 |
| **Firebase Hosting** | 10GB 存储 + 360MB 带宽/天 | 移动端 + Firebase 全家桶 | 带宽额度偏小 |
| **GitLab Pages** | 无限带宽 + 100MB 存储 | 配合 GitLab CI 使用 | 只托管公开项目 |
| **Tiiny.host** | 1 个站点 + 100 次访问/月 | 快速分享静态文件 | 容量极小 |
| **Neocities** | 1GB 存储 + 200GB 带宽/月 | 个人创意站 | 适合非技术用户 |

> **Cloudflare Pages** 的无限带宽对流量较大的站点非常友好。Vercel 专注 Next.js 体验最佳。Netlify 的 Forms 和 Functions 生态成熟。

---

## 三、Serverless 计算

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Cloudflare Workers** | 10 万请求/天 + 30 个脚本 | 边缘计算、API 网关、重定向 | 子请求限制 50 个/请求；CPU 时间 10ms 免费，超时收费 |
| **AWS Lambda** | 100 万请求/月 + 400,000 GB-秒 | AWS 生态事件驱动 | 超出后费用较高 |
| **GCP Cloud Functions** | 200 万请求/月 + 400,000 GB-秒 | GCP 生态轻量后端 | 2 代函数计费不同，注意版本选择 |
| **Azure Functions** | 100 万请求/月 + 400,000 GB-秒 | Azure 生态 + .NET 场景 | 免费层级持续提供 |
| **Deno Deploy** | 100 万请求/月 + 100GB 带宽 | 边缘 JavaScript/TypeScript | Deno 运行时兼容需注意 |
| **Vercel Edge Functions** | 50 万次/月 + 100GB 带宽 | Next.js 中间件、边缘逻辑 | 10μs 以下免费，超时计费 |
| **Netlify Functions** | 12.5 万次/月 + 100GB 带宽 | 前端项目后端逻辑 | 请求超时限制 10s（免费层） |
| **Supabase Edge Functions** | 50 万次/月 | Supabase 生态边缘函数 | 基于 Deno，和数据库深度集成 |
| **Fly.io** | 3 个共享 VM 始终免费 | Docker 容器部署 | 3 个 VM 共享资源，可能互相影响 |
| **Koyeb** | 1 个 nano 服务 (512MB RAM) | 容器化 Serverless | 免费实例会休眠 |
| **Zeabur** | 1 个服务，月流量 100GB | 国内友好，支持 Docker | 免费额度较少 |
| **Railway** | $5 额度/月 + 500 小时 | 全栈项目快速部署 | 按量计费，超出即扣钱 |

> **Cloudflare Workers** 是在边缘执行逻辑的绝佳选择，10 万请求/天足够个人项目。如果只是简单的 API 端点，一个 Worker 就能搞定。

---

## 四、后端 / PaaS

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Supabase** | 500MB PostgreSQL + 1GB 存储 + Auth + Realtime + Edge Functions | **全栈后端全家桶** | 数据库暂停机制：一周无活动暂停；暂停后需手动恢复 |
| **Firebase** | 1GB 存储 + 10GB 下载/月 + Realtime DB 1GB | 移动端后端、实时应用 | 读写次数限制严格；超出后需升级 |
| **Appwrite** | 5 个项目、500MB 存储、50GB 带宽 | 开源 BaaS 替代 | 免费层有限额，自建不受限 |
| **Nhost** | 2GB PostgreSQL + 100GB 传输 + Auth | Hasura + PostgreSQL 组合 | 基于 Hasura，GraphQL 生态 |
| **Railway** | $5 额度/月 | 快速部署全栈项目 | 需要绑卡 |
| **Render** | 750 小时/月 Web 服务 + 100GB 带宽 | Web 服务、Cron 任务 | 15 分钟无流量休眠 |
| **Fly.io** | 3 个共享 VM | Docker 容器部署 | 3 台共存，共享资源池 |
| **Koyeb** | 1 个 nano 服务 + 1 个数据库 | Serverless 容器 | 免费实例会休眠 |
| **Zeabur** | 1 服务 + 100GB 流量/月 | 国内友好部署 | 额度较紧 |
| **cyclic.sh** | 无限个免费应用（需冷启动） | 快速部署 Node.js | 5 分钟无活动休眠，冷启动慢 |
| **Adaptable** | 1 个应用 + 100GB 带宽 | Docker/模板部署 | 免费实例会休眠 |
| **Deta Space** | 无限应用 + 10GB 存储 | Python/JS 应用 | 平台较新，生态有限 |
| **Porter** | 免费开头，按需付费 | K8s 托管 | 免费额度不明确 |
| **Northflank** | 1 个微服务 + 1GB 存储 + 共享域名 | 容器化应用 | 服务会休眠 |

> **Supabase** 提供 PostgreSQL + Auth + Storage + Realtime + Edge Functions 全套能力，是当前免费 BaaS 的首选。Firebase 对移动端更友好（尤其是实时同步），但读写计费模式下用量需谨慎。

---

## 五、数据库

| 服务 | 免费额度 | 数据库类型 | 注意事项 |
|------|---------|-----------|---------|
| **Supabase PostgreSQL** | 500MB 数据库 | PostgreSQL 15/16 | 一周无活动暂停；支持 pgvector、PostGIS 扩展 |
| **Neon** | 0.5GB 数据库 + 分支功能 | Serverless PostgreSQL | 冷启动极快；自动暂停（超时可配） |
| **PlanetScale** | 5GB 存储 + 10 亿行读取/月 | MySQL 兼容 (Vitess) | 免费库无外键支持 (2019 限制)；写入 1000 行/月 |
| **MongoDB Atlas** | 512MB 存储 + 共享集群 | MongoDB 7 | 免费集群共享资源；性能有限 |
| **CockroachDB** | 10GB 存储 + 1000 RU/秒 | 分布式 PostgreSQL 兼容 | 免费层 Serverless，延迟稍高 |
| **Turso** | 9GB 总存储 + 10 亿请求/月 | 边缘 SQLite (libsql) | 每个数据库 500MB；边缘读取极快 |
| **Upstash Redis** | 10,000 命令/天 + 256MB | Redis 兼容 (Serverless) | 按命令数计费而非带宽；适合轻量缓存 |
| **AWS DynamoDB** | 25GB 存储 + 2 亿请求/月 **永免** | NoSQL 键值 | 免费额度非常慷慨；设计上需适配 NoSQL 思维 |
| **Azure Cosmos DB** | 25GB 存储 + 1000 RU/s **永免** | 多模型 (MongoDB/Cassandra/Gremlin/SQL) | 免费 1000 RU/s 够用；多区域需升级 |
| **TiDB Cloud** | 5GB 行存储 + 50MB 列存储 | MySQL 兼容分布式数据库 | 免费层自动暂停 48h 无活动 |
| **Fauna** | 100MB 存储 + 10 万请求/月 | Document + 关系混合 | GraphQL 原生支持；API 驱动 |
| **Xata** | 15GB 数据 + 15GB 存储 + 7 天历史 | PostgreSQL + Elasticsearch | 基于 PostgreSQL 但有写入限制 |
| **SingleStore** | 5GB 存储 + 10GB 缓存/月 | 分布式 SQL | 实时分析场景 |

> **DynamoDB** 和 **Cosmos DB** 的 25GB 永免是 NoSQL 领域最慷慨的。**PlanetScale** 的 5GB MySQL 免费很香但注意无外键。**Turso** 的边缘 SQLite 适合极端边缘场景。

---

## 六、对象存储 / CDN

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Cloudflare R2** | 10GB 存储 + 1000 万读/100 万写/月 + **零出站费** | 图片/文件/静态资源存储 | 全球 CDN 分发；零 egress 是最大优势 |
| **Backblaze B2** | 10GB 存储 + 1GB 下载/天 | 冷备、低成本存储 | 搭配 Cloudflare CDN 免带宽费 (Bandwidth Alliance) |
| **AWS S3** | 5GB 存储 + 20,000 GET/2000 PUT 请求/月 | AWS 生态存储 | 12 个月免费；Standard 层出站流量收费 |
| **Wasabi** | 1TB 存储 + 前 3 个月免费 | 热存储 | egress 收费；无免费层但有试用 |
| **Cloudinary** | 25 个积分/月（相当于约 25GB CDN + 1000 次变换） | 图片/视频优化 + CDN | 变换次数超限后自动收费 |
| **Imgix** | 1000 张图片 + 100GB 带宽/月 | 实时图片处理 CDN | 额度较小 |
| **Bunny.net** | 10GB 存储 + 50GB 带宽/月 | 边缘存储 + CDN | 超额费用低但需充值 |
| **Uploadcare** | 3000 文件 + 3GB 带宽/月 + 3000 次变换 | 文件上传组件 | 免费额度够原型 |
| **ImageKit** | 25GB 带宽 + 25GB 存储 | 图片处理 CDN | 超限后服务降级 |
| **ImgBB** | 1GB 存储，无限带宽 | 免费图片托管 | 不支持直接引用（可能被删） |
| **Imgur** | 无限存储（API 限制 1250 次/天） | 社交图片托管 | 不适合商业应用；可能删除内容 |
| **Cloudflare Images** | 25 万张存储 + 25 万请求/月 | 图片 CDN + 优化 | 超出额度费 0.005$/张 |
| **Storj** | 15GB 存储 + 25GB 下载/月 | 去中心化对象存储 | 基于 Blockchain，上传下载速度一般 |

> **Cloudflare R2 + Backblaze B2** 是省钱绝配：R2 零出站费做 CDN 分发，B2 和 Cloudflare 有 Bandwidth Alliance 免带宽，大量文件备份首选。

---

## 七、认证

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Clerk** | 50,000 月活跃用户 (**5万 MAU**) | 现代 Auth 组件（预构建 UI） | 限制活跃用户而非总量；邮件/短信需加钱 |
| **Auth0** | 25,000 MAU + 2 个社交登录 | 企业级身份认证 | 7,500 MAU 后品牌水印；社交登录限制 |
| **Supabase Auth** | **无限用户** | 与 PostgreSQL 深度集成 | 自带 Row Level Security；邮件服务有限 |
| **Kinde** | 7,500 MAU + 3 个 API | 简单 Auth 接入 | 超过 7,500 需付费；功能适中 |
| **WorkOS** | 100 万 MAU | 企业 SSO + Directory Sync | SSO 免费额度极高；适合 B2B |
| **Logto** | 5,000 MAU | 开源身份管理 | 自建不限用户但需服务器 |
| **SuperTokens** | 免费开源 + SuperTokens SaaS 5,000 用户 | 开源 Auth 方案 | 自建无限制；托管版有用户限制 |
| **NextAuth.js (Auth.js)** | 完全开源免费 | 原生 Next.js 集成 | 自托管，无用户限制 |
| **Keycloak** | 完全开源免费 | 企业级身份管理 | 需自托管，配置复杂 |
| **Zitadel** | 5,000 MAU | 开源 IAM，替代 Auth0 | 支持多租户 |

> **Supabase Auth** 和 Supabase 数据库紧耦合，是 PostgreSQL 项目的最佳搭配。**Clerk** 提供 5 万 MAU 非常慷慨，且预构建 UI 组件落地快。**WorkOS** 的 100 万 MAU 适合 B2B SaaS。

---

## 八、CI/CD

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **GitHub Actions** | 2000 分钟/月（私有库）；不限（公开库） | 自动化 CI/CD + 工作流 | 并发最多 20 个；macOS 分钟数单独计费 |
| **GitLab CI** | 400 分钟/月 + 5 个并行 | GitLab 生态 CI/CD | 共享 Runner；需 GitLab 账号 |
| **CircleCI** | 6,000 分钟/月（仅限 Linux） | 高并发 CI/CD | 免费层限制 30,000 次构建；macOS 需付费 |
| **Bitrise** | 200 分钟/月 | 移动端 (iOS/Android) CI | 专为移动项目设计；macOS 构建 |
| **Cloudflare Pages** | 500 次构建/月 | 静态站 + Functions | 并发 1 个构建 |
| **Vercel** | 不限构建次数 | 前端项目 | 受限于带宽 100GB/月 |
| **Netlify** | 300 分钟/月 | 前端 + Functions | 免费层 1 个并发 |
| **Jenkins** | 完全免费（自托管） | 高度自定义 CI/CD | 需要自己维护服务器 |
| **Woodpecker CI** | 完全免费（自托管） | 轻量 CI/CD | Docker 部署，资源占用低 |
| **Drone CI** | 完全免费（自托管） | 容器化 CI/CD | 已被 Harness 收购但开源版可用 |
| **Buildkite** | 250 分钟/月（代理自托管） | 混合 CI/CD 方案 | 结合自托管 Runner |

> 公开库无脑用 **GitHub Actions**。私有库 2000 分钟/月一般够用，超标的话可将非关键 CI 任务分散到 **GitLab CI** (400 分钟) 或 **Cloudflare Pages**。

---

## 九、邮件

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Resend** | 100 封/天 | 开发者友好邮件 API | 每天重置计数；支持 React Email |
| **Mailtrap** | 4000 封邮件/月 + 1 个域名 | 测试邮件发送 | 在开发/测试中广泛使用 |
| **Brevo (Sendinblue)** | 300 封/天 | 营销邮件 + Transactional | 超出需付费；不限制联系人数量 |
| **Forward Email** | 无限域名 + 10 个邮箱 | 域名邮箱（别名转发） | 完全开源；支持自定义域名 |
| **Zoho Mail** | 5 用户免费 | 企业邮箱（自定义域名） | 需验证域名；存储 5GB/用户 |
| **MailerSend** | 3000 封/月 + 1 个域名 | Transactional 邮件 | 基于 SendGrid 但有额度限制 |
| **Loops** | 1000 联系人 + 250 封/月 | Newsletter + 事务邮件 | 面向开发者，支持 API |
| **Buttondown** | 1000 订阅者 | Newsletter | 简单易用的邮件列表 |
| **Mailgun** | 1000 封/天（试用后改为按量） | Transactional 邮件 | 最多 3 个月免费；之后按量 |
| **SendGrid (Twilio)** | 100 封/天 | Transactional 邮件 | 永免但限额低；IP 信誉一般 |
| **Postmark** | 100 封/月免费试用 | 高送达率事务邮件 | 试用期短，适合测试 |
| **ProtonMail** | 1 个邮箱 + 500MB 存储 | 隐私邮件 | 不支持自定义域名 |
| **Tutanota** | 1 个邮箱 + 1GB 存储 | 加密邮件 | 不支持 IMAP/SMTP |
| **Cloudflare Email Routing** | 无限转发 | 邮件转发 + 捕获 | 配合自定义域名，仅转发不发送 |
| **iCloud+** | 自定义域名 + 5 个邮箱 | Apple 用户邮箱 | 需 iCloud+ 订阅 |
| **SimpleLogin** | 10 个别名 | 邮件别名保护隐私 | 开源，可自建 |
| **DuckDuckGo Email Protection** | 无限别名 | 隐私保护转发 | @duck.com 转发 |

> **Resend** 每天 100 封个人项目完全够用。**Forward Email** 和 **Zoho Mail** 支持自定义域名免费邮箱。**Mailtrap** 是开发测试邮件的神器。

---

## 十、错误监控

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Sentry** | 5000 事件/月 + 1 个团队 | 错误追踪 + 性能监控 | 事件超限后数据不存；性能监控另计 |
| **Datadog** | 5 台主机 + 日志 500MB/天 | APM + 基础设施监控 | 10 天保留期；需绑卡 |
| **New Relic** | 100GB 数据/月 + 1 主机免费 | 全栈可观测性 | 免费额度一直续；100GB 数据量大 |
| **Grafana Cloud** | 10k 指标 + 50GB 日志/月 + 14 天保留 | 可视化 + Prometheus 监控 | 免费层额度对个人够用 |
| **Better Stack** | 2 个心跳 + 50GB 日志/月 | 日志聚合 + 监控 | 日志保留 7 天；非常适合小项目 |
| **UptimeRobot** | 50 个监控点 (5 分钟间隔) | 网站可用性监控 | 免费层不支持 SMS 告警 |
| **Checkly** | 5 个 API + 5 个浏览器监控 | 综合监控 + Playwright 任务 | 适合前端应用 |
| **Cronitor** | 5 个心跳 + 10 个通知 | Cron 任务监控 | 监控定时任务执行 |
| **Pingdom** | 1 个监控 + 100 个告警/月 | 网站速度监控 | 免费层非常有限 |
| **Logz.io** | 1GB 日志/天 + 3 天保留 | 日志分析 (ELK) | 基于 ELK；免费层额度较小 |
| **Axiom** | 500GB 数据摄取/月 + 30 天保留 | Serverless 日志 | 对 Serverless 架构友好 |
| **Baselime** | 100GB 数据/月 + 7 天保留 | Serverless 可观测性 | 专为 Serverless 设计 |

> **Sentry** 是错误追踪的首选。**Datadog** 和 **New Relic** 是全栈监控的巨头。小项目推荐 **Better Stack** 日志 + **UptimeRobot** 监控。

---

## 十一、分析

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **PostHog** | **100 万事件/月** | 产品分析 + 自建替代 | 开源可自建；100 万免费很慷慨 |
| **Plausible** | 自建无限（开源） | 轻量隐私分析 | 自建免费但需要 VPS |
| **Plausible Cloud** | 30 天试用 + 小站计划 | 托管隐私分析 | 试用后可付费 |
| **Umami** | 自建无限（开源） | 更轻量的隐私分析 | 自建免费，资源消耗极低 |
| **Google Analytics** | 无限事件 + 标准报告 | 免费分析最全面 | 隐私合规要求严格 |
| **Microsoft Clarity** | 无限 + 无数据采样 | 会话回放 + 热力图 | 免费且功能完整 |
| **Matomo** | 自建无限（开源） | 自主可控的分析 | 功能全面，类似 GA |
| **Fathom Analytics** | 试用 30 天 | 简洁隐私分析 | 付费，无免费层 |
| **GoatCounter** | 自建无限（开源） | 极简计数器 | 最小化的网站统计 |
| **Ackee** | 自建无限（开源） | 自托管分析 | 基于 Node.js，部署简单 |
| **Counter.dev** | 免费使用 | 轻量计数分析 | 无收费计划 |
| **Heap** | 5000 会话/月 | 自动事件追踪 | 免费层限制较多 |
| **Mixpanel** | 1000 用户 + 10M 事件/月 | 用户行为分析 | 1000 用户限制严格 |

> **PostHog** 100 万事件/月 + 开源自建，是最强的免费产品分析工具。**Plausible** 自建有多轻量？一个 512MB 的 VPS 跑 Docker 就够了。**Clarity** 的无限免费会话回放是大福利。

---

## 十二、AI / 大模型

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **GitHub Copilot Free** | 每月 2000 次补全 + 50 次对话 | VS Code/Neovim/JetBrains 等 IDE | 需要 GitHub 账号；支持主流语言 |
| **Codeium (Windsurf)** | 个人免费，无限补全 | 免费 IDE AI 补全 | 无使用限制；AI Chat 免费层有限 |
| **Tabnine** | 个人免费 | AI 代码补全 | 基础补全免费 |
| **DeepSeek API** | 免费额度 + 极低价 | 国内 LLM 调用 | API 价格极低；免费额度定期更新 |
| **通义千问（阿里）** | 免费使用（200 万 tokens 试用） | 中文 LLM 推理 | Web 端免费 |
| **智谱 GLM** | 100 万 tokens/月 | 中文 LLM + API | 实名认证后可申请 |
| **百度文心一言** | 免费基础版 | 中文 LLM Web/API | API 有免费额度 |
| **Kimi（月之暗面）** | 免费 Web + App | 超长上下文问答 | 主打 200 万字上下文 |
| **豆包（字节跳动）** | 免费 Web + App | 日常 AI 助手 | 免费使用，无限制 |
| **Hugging Face** | 无限推理 + 模型托管 + 10GB 存储 | 开源模型推理/微调 | Spaces 有 CPU/GPU 额度限制 |
| **Google Colab** | 免费 GPU (T4 等，有限额) | ML 训练 + Notebook | 免费 GPU 有时间限制（约 12h） |
| **Cloudflare Workers AI** | 10 万次/天 | 边缘 AI 推理 | 模型有限（Llama 2、Mistral 等） |
| **Replicate** | 免费试用 $5 额度 | 云上模型推理 | 试用额度用完需付费 |
| **Groq** | 免费 API 推理 | 极速 LLM 推理 (LPU) | 免费层请求频率限制 |
| **Perplexity** | 免费 Web + App | AI 搜索 + 推理 | 免费用户每日有限查询 |
| **Claude.ai** | 免费 Web (有限额) | 对话 | 免费用户消息频率限制 |
| **ChatGPT** | 免费 Web + App | 通用 AI 对话 | 功能受限于 GPT-4o mini |
| **Google Gemini** | 免费 Web + App + API | 多模态 AI | API 免费有速率限制 |
| **Mistral AI** | 免费 API（有限额） | LLM API | 开源模型平台 |
| **Together AI** | $0.10 试用额度 | 分布式 AI 推理 | 试用金用完即止 |
| **Vercel AI SDK** | 免费 + 按量（AI 路由） | AI 应用开发框架 | 框架免费，但调用 API 需付费 |

> 代码助手 **GitHub Copilot Free** 和 **Codeium** 是两大主力。国内大模型 **DeepSeek**、**通义千问**、**GLM** 等均提供免费 API 额度。**Google Colab** 的免费 GPU 对学习 ML 仍然是最佳选择。

---

## 十三、CMS / Headless CMS

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Strapi** | 自建完全免费开源 | 自托管 Headless CMS | 需要服务器运行；功能全面 |
| **Strapi Cloud** | 免费试用（有限额） | 托管 Strapi | 试用后付费 |
| **Contentful** | 3 用户 + 500 条内容 + 2 个环境 | SaaS Headless CMS | 内容条数限制；支持 Webhook |
| **Sanity** | 3 用户 + 1 个项目 + 无限内容 + 100GB CDN | 实时协作 CMS | 付费层按使用量；免费层可无限内容 |
| **TinaCMS** | 开源免费 + Tina Cloud 1 个项目 | Git-backed CMS | 编辑内容直接提交到 Git |
| **Ghost** | 自建免费（开源） | 博客/会员系统 | 托管版 Ghost(Pro) 需付费 |
| **WordPress** | 自建免费 + WordPress.com 免费子域名 | 传统 CMS | 需服务器自建 |
| **Hygraph** | 1 个项目 + 100 万 API 调用/月 | GraphQL CMS | 免费层限额较高 |
| **Directus** | 自建免费（开源） | 数据库优先后端/CMS | 支持 SQL 数据库 |
| **Payload CMS** | 自建免费（开源） | TypeScript CMS | 需要 Node.js 部署 |
| **Decap CMS (Netlify CMS)** | 免费（Git-based） | 静态站 CMS | 连接 Git 仓库，完全免费 |
| **Cosmic** | 1 个项目 + 50GB 带宽 | 用户友好的 CMS | 免费层有限制 |
| **Storyblok** | 1 个用户 + 250 条内容 | 可视化编辑 CMS | 内容条数限制 |

> 自建无限用 **Strapi**、**Directus** 或 **Payload CMS**。SaaS 使用 **Sanity** 免费额度最慷慨。Git-backed 场景 **TinaCMS** 和 **Decap CMS** 是 JAMStack 的最佳拍档。

---

## 十四、搜索

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Algolia** | 10,000 条记录 + 10,000 次搜索/月 + 100k 次操作 | 全文搜索（前端优先） | 超出后费用较高；API 密钥暴露需注意 |
| **Meilisearch** | 自建免费（开源） + Meilisearch Cloud 1GB 存储 | Rust 全文搜索引擎 | 自建无限制；速度快 |
| **Typesense** | 自建免费（开源） + Typesense Cloud 7 天试用 | 轻量全文搜索 | 类似 Algolia 的开源替代 |
| **Elasticsearch** | 自建免费（开源） | 企业级搜索分析 | 资源消耗大 |
| **Elastic Cloud** | 14 天试用 | 托管 Elasticsearch | 试用期短 |
| **Sonic** | 自建免费（开源） | 极简搜索后端 | Rust 编写，资源轻 |
| **TinySearch** | 自建免费（开源） | 极简搜索 | 适合小网站 |
| **Typesense Cloud** | 试用 | 托管搜索 | 试用后需付费 |

> 自建搜索推荐 **Meilisearch**（功能最全的开源搜索）或 **Typesense**（Algolia 最佳替代）。SaaS 用 **Algolia** 免费层 1 万条记录。

---

## 十五、DNS / 安全

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Cloudflare DNS** | 无限域名 + DNS 解析 + DDoS 防护 + CDN | **DNS + CDN + DDoS 三合一** | 全球最快 DNS 之一；免费层包含业界顶级 DDoS 防护 |
| **Let's Encrypt** | 无限免费 SSL 证书 | **自动化 SSL 证书** | 90 天有效，需自动续期 |
| **ZeroSSL** | 3 个免费 SSL 证书（90 天） | 手动 SSL 证书 | 比 LE 多一个管理界面 |
| **SSL.com** | 30 天试用 | 付费 SSL | 试用短暂 |
| **Cloudflare Tunnel (Argo Tunnel)** | 免费 | 内网穿透 + 无公网 IP 暴露 | 无需开放端口，零信任安全 |
| **Cloudflare WAF** | 免费基础规则 | Web 应用防火墙 | 免费层有流量限制 |
| **Cloudflare Turnstile** | 无限免费 | CAPTCHA 替代 | 替代 reCAPTCHA，无验证限制 |
| **hCaptcha** | 免费 | CAPTCHA | 隐私友好的验证码 |
| **DuckDNS** | 免费 DDNS | 动态 DNS | 完全免费 |
| **FreeDNS (Afraid.org)** | 免费 | DNS 托管 | 社区维护 |
| **dnspod.cn (腾讯)** | 免费 DNS 解析 | 国内 DNS | 解析快，适合国内站点 |

> **Cloudflare DNS + Let's Encrypt + Cloudflare Tunnel** 组合 = 零成本网络基础设施。**Cloudflare Turnstile** 替代 Google reCAPTCHA 无需付费且保护隐私。

---

## 十六、设计 / 协作

| 服务 | 免费额度 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **Figma** | 无限个人文件 + 3 个项目 | UI/UX 设计、原型 | 草稿无限，团队项目限制 3 个 |
| **Canva** | 免费使用 250,000+ 模板 | 平面设计、社交图 | Pro 资源需付费 |
| **Excalidraw** | 完全免费 | 白板/流程图 | 开源；支持实时协作 |
| **Penpot** | 完全免费（开源） | UI/UX 设计 | Figma 开源替代 |
| **Draw.io (diagrams.net)** | 完全免费 | 流程图/架构图 | 可离线使用 |
| **Linear** | 250 个 Issue + 团队 | 项目管理/Issue 追踪 | 超过 250 个 Issue 需升级 |
| **Notion** | 个人免费 | 文档/笔记/项目管理 | 团队空间有限制 |
| **Miro** | 3 个白板 | 在线白板协作 | 免费版项目有限 |
| **Trello** | 10 个看板 + 1 个插件 | 看板项目管理 | 功能基本够用 |
| **ClickUp** | 100MB 存储 + 不限任务 | 全功能项目管理 | 功能多但略重 |
| **Milanote** | 有限免费 | 灵感板/创意工具 | 免费额度少 |
| **Excalidraw+** | 免费基础功能 | 协作白板 | Excalidraw 增强版 |
| **Tldraw** | 完全免费（开源） | 在线白板 | 轻量、可嵌入 |
| **Reactive Resume** | 免费使用 | 简历制作 | 开源简历工具 |
| **Coolors** | 免费色板生成 | 配色方案 | 可导出调色板 |

> 设计 **Figma** 仍然是行业标准。白板用 **Excalidraw** 或 **Tldraw**。项目管理 **Linear** 免费 250 个 Issue 够小团队使用。

---

## 十七、教育 / 学生福利

| 服务 | 学生福利 | 适用场景 | 注意事项 |
|------|---------|---------|---------|
| **GitHub Student Pack** | **$200+ 免费额度**，含 AWS/Azure/Stripe/Namecheap/Netlify/Sentry 等数十项服务 | 学生开发者工具合集 | 需要学校邮箱或学生证件验证 |
| **JetBrains** | 学生可免费使用全系列 IDE（IntelliJ / PyCharm / WebStorm 等） | 专业 IDE 开发 | 需学生邮箱注册，每年验证一次 |
| **Azure for Students** | **$100/年** Azure 额度 + 免费开发工具 | 云计算学习 | 需学校邮箱；无需信用卡 |
| **GitHub Copilot** | 学生免费使用 | AI 编程助手 | 在 GitHub Education 内激活 |
| **GitHub Pro** | 学生免费 | 私人仓库 + Actions 更多额度 | 跟随 Student Pack |
| **GitLab** | 学生免费 Ultimate 版（1 年） | CI/CD 全功能 | 需验证学生身份 |
| **DigitalOcean** | $100 额度（学生） | VPS 部署 | 通过 GitHub Student Pack |
| **Namecheap** | 1 年免费 .me 域名 + SSL | 域名注册 | Student Pack 提供 |
| **Name.com** | 1 年免费域名 | 域名注册 | 部分域名需要 Student Pack |
| **Autodesk** | 学生免费使用全系软件（AutoCAD / Maya / 3ds Max 等） | CAD/3D 建模 | 需学校邮箱验证；1 年有效期 |
| **Figma** | 学生专业版免费 2 年 | 设计工具全功能 | 需学校邮箱 |
| **Notion** | 学生 Plus 版免费 | 笔记/知识库 | 需学校邮箱 |
| **Google Workspace** | 学生免费使用 | 协作办公 | 学校邮箱一般可激活 |
| **Apple** | 学生优惠购买 Mac/iPad | 硬件 | 需验证学生身份 |
| **Spotify** | 学生半价 Premium | 音乐 | 需验证学生身份 |
| **Amazon Prime Student** | 6 个月免费，之后半价 | 购物/视频 | 需学校邮箱 |

> **GitHub Student Pack** 是学生必须申请的第一张"卡"——$200+ 免费额度覆盖云计算、域名、IDE 等。**JetBrains** 全系 IDE 学生免费，对专业开发者极有价值。**Autodesk** 全系 CAD/3D 软件学生免费使用。

---

## 十八、其他

| 工具 | 许可证 | 用途 |
|------|-------|------|
| **Android Studio** | 完全免费 | Android 应用开发 IDE |
| **VS Code** | 完全免费开源 | 通用代码编辑器 |
| **Git** | 完全免费开源 | 版本控制 |
| **Bruno** | 完全免费开源 | API 客户端（Postman 替代） |
| **Obsidian** | 个人免费 | 知识管理 / 笔记 |
| **Postman** | 免费：3 人协作 + 3 集合 | API 测试 |
| **Insomnia** | 免费使用 | API 客户端（开源） |
| **Hoppscotch** | 完全免费开源 | 在线 API 测试 |
| **DBeaver** | 免费社区版 | 数据库 GUI 管理 |
| **TablePlus** | 免费：2 个窗口 | 数据库 GUI |
| **pgAdmin** | 完全免费开源 | PostgreSQL 管理 |
| **Redis Insight** | 完全免费 | Redis GUI |
| **MongoDB Compass** | 完全免费 | MongoDB GUI |
| **Docker Desktop** | 个人免费 | 容器化开发 |
| **Podman** | 完全免费开源 | Docker 替代 |
| **Kubernetes (Minikube)** | 完全免费开源 | 本地 K8s |
| **Nginx** | 完全免费开源 | Web 服务器 / 反向代理 |
| **Caddy** | 免费开源（个人） | Web 服务器（自动 HTTPS） |
| **Homebrew** | 完全免费开源 | macOS/Linux 包管理器 |
| **Zsh + Oh My Zsh** | 完全免费开源 | Shell 增强 |
| **tmux** | 完全免费开源 | 终端复用器 |
| **Vim / Neovim** | 完全免费开源 | 终端编辑器 |
| **ffmpeg** | 完全免费开源 | 音视频处理 |
| **ImageMagick** | 完全免费开源 | 图片处理 |
| **Pandoc** | 完全免费开源 | 文档格式转换 |
| **Ollama** | 完全免费开源 | 本地运行 LLM |
| **LangChain** | 完全免费开源 | LLM 应用框架 |
| **Playwright** | 完全免费开源 | 端到端测试 |
| **Cypress** | 免费开源 | 前端测试 |
| **Vitest** | 免费开源 | 单元测试 |
| **pnpm** | 免费开源 | 快速包管理器 |
| **Bun** | 免费开源 | JavaScript 运行时 + 包管理 |
| **Astro** | 免费开源 | 内容网站框架 |
| **Next.js** | 免费开源 | React 全栈框架 |
| **Nuxt** | 免费开源 | Vue 全栈框架 |
| **Hono** | 免费开源 | 轻量 Web 框架（边缘友好） |
| **Express** | 免费开源 | Node.js 后端框架 |
| **Fastify** | 免费开源 | 高性能 Node.js 框架 |
| **Flask** | 免费开源 | Python Web 框架 |
| **FastAPI** | 免费开源 | Python 高性能 API 框架 |
| **Gin** | 免费开源 | Go Web 框架 |
| **Rust** | 免费开源 | 系统编程语言 |
| **Zig** | 免费开源 | 系统编程语言 |
| **Go** | 免费开源 | 编程语言 |
| **SQLite** | 公共领域 | 嵌入式数据库 |
| **PostgreSQL** | 免费开源 | 关系数据库 |
| **Redis** | 免费开源（BSD） | 缓存 / 消息队列 |
| **NATS** | 免费开源 | 消息队列 |
| **RabbitMQ** | 免费开源 | 消息队列 |
| **Kafka** | 免费开源 | 事件流平台 |
| **Prometheus** | 免费开源（CNCF） | 监控 / 时间序列 DB |
| **Grafana** | 免费开源 | 数据可视化 |
| **Traefik** | 免费开源 | 反向代理 / 网关 |
| **Hasura** | 免费开源 | GraphQL 引擎 |

---

## 推荐组合：零成本搭建全栈应用

以下组合覆盖了不同场景，全部 **每月 0 元**：

### 个人博客 / 文档站

```
Cloudflare Pages   → 无限带宽托管
+ Cloudflare R2    → 图片/文件存储（零出站费）
+ Cloudflare DNS   → DNS + DDoS 防护
+ Let's Encrypt    → 免费 SSL
+ GitHub Actions   → CI/CD（公开库无限）
+ Umami（自建）    → 轻量分析
+ Forward Email    → 自定义域名邮箱
= 每月 0 元
```

### 全栈 SaaS 应用

```
Vercel / Cloudflare Pages  → 前端托管
+ Supabase                → PostgreSQL + Auth + Storage + Realtime
+ Cloudflare R2           → 文件存储（无出站费）
+ Resend                  → 事务邮件（100 封/天）
+ Sentry                  → 错误监控（5000 事件/月）
+ Clerk                   → 认证（5 万 MAU）
+ PostHog                 → 产品分析（100 万事件/月）
+ GitHub Actions          → CI/CD
+ Cloudflare Workers      → 边缘函数
= 每月 0 元
```

### AI / LLM 应用

```
Vercel / Cloudflare Pages   → 前端
+ Cloudflare Workers AI    → 边缘推理（10 万次/天）
+ Supabase                → 存储对话 + 用户数据
+ DeepSeek API            → LLM 推理（免费额度）
+ Hugging Face            → 模型托管
+ Upstash Redis           → 缓存/速率限制
+ GitHub Copilot Free     → 写代码
= 每月 0 元
```

### 学习 / 实验环境

```
Oracle Cloud Always Free   → 4 核 ARM + 24GB RAM（VPS 永免）
+ GitHub Student Pack      → $200+ 额度
+ Google Colab             → 免费 GPU
+ JetBrains（学生）        → 专业 IDE
+ VS Code                  → 编辑器
+ Docker                   → 容器化部署
= 每月 0 元
```

### 移动端 MVP

```
Firebase              → Auth + Firestore + Storage + Hosting
+ Appwrite            → 备用 BaaS
+ Android Studio      → 免费 IDE
+ Bitrise             → 移动 CI/CD（200 分钟/月）
+ Figma               → 设计原型
+ Clerk               → 用户认证
= 每月 0 元
```

---

## 省钱策略总结

1. **能自建就自建** — Strapi、Plausible、Umami、Meilisearch、Supabase 等都开源，自建无上限
2. **选对"无限"服务** — Cloudflare Pages（无限带宽）、Cloudflare Workers（10 万/天）、PostHog（100 万事件/月）、Supabase Auth（无限用户）
3. **善用 Bandwidth Alliance** — Backblaze B2 + Cloudflare 免出站费
4. **Oracle ARM 做重型计算** — 4 核 24GB 永免，跑 Docker 全家桶
5. **学生身份最大化** — GitHub Student Pack + JetBrains + Azure for Students + Autodesk
6. **信用卡备老号** — Oracle、AWS、Azure 等均需信用卡验证，但额度用完后可以降级到免费层
7. **永远设告警** — 任何绑卡服务都要设置预算告警，防止意外超量

## 写在最后

2026 年的免费云服务生态已经相当成熟。关键在于**选对组合**——把计算、存储、数据库、认证、CI/CD、监控、分析的需求分解到不同服务上，利用各自的免费额度，完全可以零成本搭建并运行一个全栈应用。

本文持续更新中。如果你发现了新的优质免费服务，或者某个服务的免费政策有变化，欢迎提 PR 或 Issue 补充。

Happy building! 🚀
