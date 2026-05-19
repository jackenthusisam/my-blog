---
date: '2026-05-20T00:30:00+08:00'
title: '我是如何搭建这个博客的'
tags: ["教程", "Hugo", "Cloudflare"]
---

## 前言

2026年5月20日，我决定搭建一个自己的博客。整个过程从零开始，花了不到 30 分钟。

本文记录完整的搭建过程。

## 方案选择

- **框架**: Hugo（极速静态网站生成器）
- **托管**: Cloudflare Pages（免费，自动部署）
- **代码托管**: GitHub
- **主题**: PaperMod

Hugo 是一个用 Go 语言编写的静态网站生成器。你只需要写 Markdown 文章，Hugo 会自动将它们转换成 HTML 网页。

Cloudflare Pages 连接 GitHub 仓库后，每次推送代码都会自动构建和部署，完全自动化。

## 步骤一：安装 Hugo

在本地安装 Hugo：

```bash
# Linux 环境
wget https://github.com/gohugoio/hugo/releases/download/v0.147.0/hugo_extended_0.147.0_linux-amd64.tar.gz
tar -xzf hugo_extended_0.147.0_linux-amd64.tar.gz hugo
sudo mv hugo /usr/local/bin/hugo
hugo version
```

## 步骤二：创建站点

```bash
hugo new site my-blog --force
cd my-blog
git init
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
```

## 步骤三：配置主题

修改 `hugo.toml` 配置文件，设置主题为 PaperMod，并配置博客标题、菜单等。

```toml
baseURL = 'https://你的用户名.pages.dev/'
languageCode = 'zh-cn'
title = '我的博客'
theme = 'PaperMod'
# ... 更多配置
```

## 步骤四：写第一篇文章

```bash
hugo new content posts/hello-world.md
```

编辑 Markdown 文件即可写文章。

## 步骤五：部署到 Cloudflare Pages

1. 将代码推送到 GitHub 仓库
2. 登录 Cloudflare Dashboard → Workers & Pages → 创建 Pages 项目
3. 连接 GitHub 仓库
4. 框架预设选择 Hugo（或手动填：构建命令 `hugo`，输出目录 `public`）
5. 保存并部署

## 日常工作流

以后写文章只需要：

```bash
hugo new content posts/文章标题.md
# 编辑 content/posts/文章标题.md
git add -A
git commit -m "新文章"
git push
```

推送到 GitHub 后，Cloudflare 会自动构建并部署，约 1-2 分钟即可在线上看到更新。

## 在手机上/网页上写文章

也可以直接在 GitHub 网站上编辑 `content/posts/` 目录下的文件，提交后同样会自动部署。

## 总结

- **费用**: 0 元（GitHub + Cloudflare 免费计划）
- **服务器**: 不需要，纯静态托管
- **维护**: 几乎为零，只管写文章就行
- **域名**: 默认使用 `xxx.pages.dev` 免费域名，也可以绑定自己的域名
