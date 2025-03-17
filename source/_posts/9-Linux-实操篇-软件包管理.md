---
title: 📦 9-Linux 实操篇 - 软件包管理 🚀
date: 2025-03-20 16:00:00
categories: [Linux]
tags: [Linux, 软件管理, apt, dpkg, 源码安装, 包管理, Snap]
author: "kkyu9527"
cover: /images/LinuxNode/LinuxNodeCover.png
---

# 📦 9-Linux 实操篇 - 软件包管理 🚀

## 🎯 9.1 软件包管理简介

Linux 软件包管理主要分为两种类型：

- 📦 **二进制包**：预编译的包，安装快捷，适用于大部分用户。
- 🛠️ **源码包**：需用户手动编译安装，灵活性高，适合高级用户。

本篇以 **Ubuntu系统** 为例，重点介绍 `apt`、`dpkg` 和源码安装方式。

---

## ⚡ 9.2 Ubuntu 软件管理工具介绍

Ubuntu 常用的工具：

- 🔧 `apt`（推荐）：自动管理软件依赖关系，安装简单便捷。
- 🔨 `dpkg`：底层管理工具，适合单独的 `.deb` 文件安装。

## 🛠 9.3 apt 常用命令

### 📌 9.2.1 apt 更新和安装软件

```shell
sudo apt update       # 更新软件列表
sudo apt upgrade       # 升级软件到最新版本
sudo apt install vim   # 安装vim编辑器
```

### 📌 9.2.2 删除与清理软件

```shell
sudo apt remove vim      # 卸载软件但保留配置文件
sudo apt purge vim       # 完全卸载软件和配置文件
sudo apt autoremove      # 自动清理未使用的软件依赖
```

### 📌 9.2.3 常用查询指令

```shell
apt search 软件名        # 搜索软件
apt show vim             # 查看软件详情
```

## 🧩 9.3 dpkg 工具详解

`dpkg` 是更底层的软件包管理工具，适合处理单独的 `.deb` 文件。

### 📌 9.3.1 常用命令

```shell
sudo dpkg -i 软件名.deb     # 安装deb包
sudo dpkg -r 软件名          # 删除软件包但保留配置
sudo dpkg -P 软件名         # 完全删除软件和配置
```

### 📌 9.3.2 查询安装的软件

```shell
dpkg -l | grep 软件名      # 查看软件包安装情况
```

## 🔄 9.4 软件源配置与更新

推荐使用国内镜像提高下载速度。

### 📌 9.4.1 更改为阿里云镜像

编辑配置文件：

```shell
sudo vim /etc/apt/sources.list
```

替换以下内容：

```shell
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
```

更新源：
```shell
sudo apt update
```

## ⚙️ 9.5 源码编译安装软件

当无法使用二进制包时，可使用源码编译方式。

### 📌 9.5.1 源码安装基本步骤

```shell
wget http://nginx.org/download/nginx-1.20.0.tar.gz
tar -zxvf nginx-1.20.0.tar.gz
cd nginx-1.20.0
./configure
make
sudo make install
```

### 📌 9.5.2 编译安装注意事项

- 安装依赖工具：
```shell
sudo apt install build-essential
```

- 编译过程中可能需要安装其他库文件，遇到问题注意查看报错信息。

## 📂 9.6 Snap 软件包管理工具（扩展）

Snap 提供了一种便捷、安全的软件安装方式。

### 📌 9.6.1 基本用法

```shell
snap install 软件名    # 安装软件
snap list              # 查看已安装软件
snap remove 软件名     # 卸载软件
```

## 🛡️ 9.7 软件管理的常见问题与解决

- **依赖问题解决方法**：

```shell
sudo apt install -f
```

- **dpkg安装包依赖问题**：

```shell
sudo dpkg -i 软件名.deb
sudo apt install -f
```

## 🎯 9.8 最佳实践总结

- 推荐日常使用 `apt`。
- 了解 `dpkg` 处理特殊情况。
- 源码安装适用于特殊定制需求。
- 定期维护软件，确保系统安全稳定。
