---
title: 🚀 GitHub Actions 自动部署 Hexo
date: 2025-03-17 21:00:00
categories: [技术分享]
tags: [GitHub Actions, Hexo, CI/CD]
author: "kkyu9527"
cover: 
---

# 🚀 GitHub Actions 自动部署 Hexo

## 🎯 1. 为什么要用 GitHub Actions 部署 Hexo？

Hexo 是一个高效的静态博客框架，而 GitHub Pages 提供了免费托管。但每次更新博客时，需要手动执行 `hexo clean && hexo g && hexo d`，比较繁琐。使用 **GitHub Actions**，可以实现：

✅ **自动化部署**：推送代码后，自动生成静态文件并发布到 GitHub Pages。
✅ **持续集成 (CI/CD)**：确保博客始终可用，减少人为错误。
✅ **无需本地环境**：不再需要在本地运行 Hexo 相关命令，任何设备都能更新博客。

---

## 🔧 2. 配置 GitHub Actions 自动部署 Hexo

### 🛠 2.1 创建 GitHub 仓库

首先，确保你的 Hexo 博客已经上传到 GitHub，并且 **源代码** 存放在 `main` 分支。

**示例仓库结构：**
```plaintext
├── source/         # 博客文章
├── themes/         # 主题文件
├── _config.yml     # Hexo 配置文件
├── package.json    # 依赖管理
└── ...
```

---

### 🔑 2.2 生成 GitHub Token（部署权限）

GitHub Actions 需要权限来推送生成的静态文件到 `gh-pages` 分支。

1️⃣ **进入 GitHub 个人设置** -> **Settings** -> **Developer settings** -> **Personal access tokens**
2️⃣ 点击 **Generate new token**，勾选 `repo` 权限。
3️⃣ 生成 Token 并复制（**注意：只显示一次，务必保存！**）。

然后，进入 **GitHub 仓库**：
- 打开 **Settings** -> **Secrets and variables** -> **Actions**
- 点击 **New repository secret**，创建一个新密钥：
  - **Name:** `HEXO_DEPLOY_KEY`
  - **Value:** 你的 GitHub Token

---

### 📜 2.3 创建 GitHub Actions 工作流

在 **Hexo 源代码仓库** 中，新建 **GitHub Actions 配置文件**：

**📁 路径：** `.github/workflows/deploy.yml`

**📜 配置内容：**
```yaml
name: Hexo Deploy

on:
  push:
    branches:
      - main  # 监听 main 分支推送事件

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: 🛎️ 拉取代码
        uses: actions/checkout@v3
        with:
          submodules: true  # 拉取主题子模块

      - name: 📦 安装 Node.js 环境
        uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: 'npm'

      - name: 📦 安装 Hexo 依赖
        run: |
          npm install -g hexo-cli
          npm install

      - name: 🚀 生成静态文件
        run: |
          hexo clean
          hexo generate

      - name: 🔑 部署到 GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.HEXO_DEPLOY_KEY }}
          publish_dir: ./public
```

**配置解析：**
- **监听 `main` 分支的 push 事件**，每次更新博客都会触发部署。
- **拉取仓库代码**，包含主题子模块（如 Butterfly 主题）。
- **安装 Node.js 和 Hexo 依赖**，确保环境完整。
- **执行 `hexo clean && hexo generate`**，生成静态文件。
- **使用 `peaceiris/actions-gh-pages` 自动推送**，将 `public/` 目录部署到 `gh-pages` 分支。

---

### 🚀 2.4 启用 GitHub Pages

在 **GitHub 仓库** -> **Settings** -> **Pages** 配置：
1. **Branch:** 选择 `gh-pages`（如果没有则先创建）
2. **Save**

等待 GitHub Actions 运行完成后，即可访问你的博客：
```
https://你的用户名.github.io/
```

---

## 🛠 3. 常见问题及优化

### ❓ 3.1 Hexo 主题无法拉取？
如果使用了 `git submodule` 但 GitHub Actions 没有拉取，可以手动执行：
```yaml
- name: 拉取子模块
  run: git submodule update --init --recursive
```

### ❓ 3.2 GitHub Actions 执行失败？
1️⃣ 检查 `.github/workflows/deploy.yml` 是否正确。
2️⃣ 确保 **GitHub Token 有 repo 权限**，并正确配置在 `secrets.HEXO_DEPLOY_KEY`。
3️⃣ 查看 **GitHub Actions 运行日志**，修复错误。

### ❓ 3.3 如何加速 Hexo 生成？
- 使用 `hexo clean && hexo g --watch` 只生成变更部分。
- 在 `.gitignore` 中排除 `node_modules/` 目录，加快 `npm install`。

---

## 🎉 4. 总结

✅ **自动部署 Hexo 到 GitHub Pages**
✅ **借助 GitHub Actions 实现 CI/CD**
✅ **提高效率，避免手动执行部署命令**

配置完成后，每次更新博客，只需 `git push`，GitHub Actions 就会自动完成构建和部署，让你的博客随时保持最新！ 🚀✨

---

📌 **完整代码示例已提供，按步骤操作即可实现自动部署！** 🎯

