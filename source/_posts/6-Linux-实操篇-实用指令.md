---
title: 🛠 6-Linux 实操篇 - 实用指令

date: 2025-03-19 10:00:00
categories: [Linux]
tags: [Linux, 运行级别, 用户管理, 文件操作, 压缩解压]
author: "kkyu9527"
cover: /images/LinuxNode/LinuxNodeCover.png
---

# 🛠 6-Linux 实操篇 - 实用指令

## 🎯 6.1 指定运行级别

### 📌 6.1.1 运行级别介绍

| 级别 | 说明                       |
|----|--------------------------|
| 0  | 关机                       |
| 1  | 单用户模式（用于恢复系统或找回密码）       |
| 2  | 多用户模式（无网络）               |
| 3  | **多用户模式（有网络）** 🏆（服务器常用） |
| 4  | 预留（未使用）                  |
| 5  | **图形界面模式** 🖥（桌面系统常用）    |
| 6  | **系统重启** 🔄              |

### 📌 6.1.2 切换运行级别

```bash
init [0123456]  # 立即切换到指定运行级别
```

📌 **示例：** 切换到 **多用户模式（无 GUI）**
```bash
init 3
```

📌 **查看当前运行级别**
```bash
systemctl get-default
```

📌 **设置默认运行级别**
```bash
systemctl set-default multi-user.target  # 设置为多用户模式
systemctl set-default graphical.target  # 设置为图形界面模式
```

---

## 🔑 6.2 找回 Root 密码

### 📌 6.2.1 恢复 Root 密码步骤

1️⃣ **重启系统，并按 `Shift` 进入 GRUB 菜单**
2️⃣ 选择 **Advanced options for Ubuntu** 并按 `Enter`
3️⃣ 选择 **Recovery mode** 进入 **Recovery Menu**
4️⃣ 选择 **root - Drop to root shell prompt**
5️⃣ 在 Shell 中输入：
```bash
passwd root  # 重新设置 root 密码
```
6️⃣ 输入新密码并确认
7️⃣ **重启系统**
```bash
reboot
```

---

## 📖 6.3 获取命令帮助

### 📌 6.3.1 `man` 命令
```bash
man ls  # 查看 ls 命令的详细帮助信息
```

### 📌 6.3.2 `help` 命令
```bash
help cd  # 获取 shell 内置命令的帮助
```

---

## 📂 6.4 文件与目录操作

### 📌 6.4.1 `pwd` - 显示当前目录
```bash
pwd
```

### 📌 6.4.2 `ls` - 列出目录内容
```bash
ls -a   # 显示所有文件（包括隐藏文件）
ls -l   # 以详细信息显示文件
```

### 📌 6.4.3 `cd` - 切换目录
```bash
cd /root  # 进入 root 目录
cd ..     # 返回上一级目录
cd ~      # 返回家目录
```

### 📌 6.4.4 `mkdir` - 创建目录
```bash
mkdir -p /home/animal/tiger  # 创建多级目录
```

### 📌 6.4.5 `rmdir` - 删除空目录
```bash
rmdir /home/dog  # 只能删除空目录
```

### 📌 6.4.6 `touch` - 创建空文件
```bash
touch hello.txt
```

### 📌 6.4.7 `rm` - 删除文件或目录
```bash
rm -r /home/bbb  # 递归删除整个目录
```

### 📌 6.4.8 `mv` - 移动/重命名文件
```bash
mv old.txt new.txt  # 重命名文件
mv file /home/user  # 移动文件
```

### 📌 6.4.9 `cat` - 查看文件内容
```bash
cat -n /etc/profile  # 显示行号
```

---

## 🛠 6.5 搜索与查找

### 📌 6.5.1 `find` - 查找文件
```bash
find /home -name hello.txt  # 在 /home 目录下查找 hello.txt
```

### 📌 6.5.2 `grep` - 文本搜索
```bash
grep -n "yes" /home/hello.txt  # 查找包含 "yes" 的行，并显示行号
```

---

## 🗜 6.6 压缩与解压

### 📌 6.6.1 `gzip/gunzip` - 压缩/解压 `.gz` 文件
```bash
gzip file.txt  # 压缩 file.txt 生成 file.txt.gz
gunzip file.txt.gz  # 解压 file.txt.gz
```

### 📌 6.6.2 `zip/unzip` - 压缩/解压 `.zip` 文件
```bash
zip archive.zip file.txt  # 压缩文件
unzip archive.zip  # 解压 zip 文件
```

### 📌 6.6.3 `tar` - 压缩/解压 `.tar.gz` 文件
```bash
tar -zcvf archive.tar.gz /home/user  # 压缩目录

tar -zxvf archive.tar.gz -C /opt/tmp2  # 解压到指定目录
```

---

## ⏳ 6.7 时间管理

### 📌 6.7.1 `date` - 显示/设置时间
```bash
date "2025-03-19 10:00:00"  # 设置系统时间
```

### 📌 6.7.2 `cal` - 显示日历
```bash
cal 2024  # 显示 2024 年日历
```

---

## 🎉 6.8 总结

✅ **掌握运行级别控制，学会找回 Root 密码**。
✅ **熟练使用 `ls`、`cd`、`rm`、`mv` 进行文件管理**。
✅ **掌握 `find`、`grep` 进行文件和文本搜索**。
✅ **掌握 `tar`、`zip` 进行文件压缩和解压**。
✅ **学会 `date`、`cal` 进行时间管理**。
