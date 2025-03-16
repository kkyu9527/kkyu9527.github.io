---
title: 我的第一篇博客
date: 2025-03-16 11:00:00
tags: [Hexo, 博客, 技术]
categories: [前端]
---

# 我的 Hexo 博客

欢迎访问我的个人博客 [kkyu9527.github.io](https://kkyu9527.github.io/)！这里记录了我的技术笔记、学习心得以及日常分享。

## 🚀 快速开始

### 1️⃣ 本地运行博客
本地启动博客，请按照以下步骤操作：
```bash
hexo clean && hexo g && hexo s
```
然后在浏览器中打开：
```
http://localhost:4000
```

### 2️⃣ 发布博客到 GitHub Pages
写完一篇新文章后，可以使用以下命令生成静态文件并部署到 GitHub Pages：
```bash
hexo clean && hexo g && hexo d
```
然后在浏览器中访问：
```
https://kkyu9527.github.io/
```

## 📖 目录结构
```
.
├── _config.yml            # Hexo 配置文件
├── package.json           # 依赖包管理文件
├── themes/                # 主题文件夹
├── source/                # 文章存放目录
│   ├── _posts/            # Markdown 文章
│   ├── images/            # 图片存放目录
│   └── about.md           # 关于页面
├── public/                # 生成的静态文件
└── scaffolds/             # 文章模板
```

## ✍️ 如何新建文章
```bash
hexo new "文章标题"
```
然后在 `source/_posts/` 目录下编辑生成的 Markdown 文件。

## 🎨 更换博客主题
目前使用的主题是 **Butterfly**，你可以切换其他 Hexo 主题：
```bash
git clone -b master https://gitee.com/immyw/hexo-theme-butterfly.git themes/butterfly
```
然后修改 `_config.yml` 文件中的 `theme` 选项：
```yaml
theme: butterfly
```

## 🔧 常见问题

### 1. GitHub Pages 无法显示最新的内容？
✅ **检查 GitHub Pages 是否启用**
1. 进入 GitHub 仓库：  
   👉 [GitHub 仓库](https://github.com/kkyu9527/kkyu9527.github.io)
2. 进入 **Settings** -> **Pages**，确保 **Source** 选择的是 `main` 分支。

✅ **重新部署 Hexo**
```bash
hexo clean && hexo g && hexo d
```

✅ **检查 `.nojekyll` 文件**
```bash
touch public/.nojekyll
hexo d
```

### 2. 如何查看 Hexo 的日志？
如果你在 `hexo g` 或 `hexo d` 过程中遇到错误，可以查看 Hexo 生成的日志：
```bash
hexo g --debug
```

## 🎯 未来计划
- [ ] 优化博客界面
- [ ] 添加搜索功能
- [ ] 增加更多技术分享内容

💡 **如果你有任何建议或问题，欢迎提交 Issue 或 PR！**

