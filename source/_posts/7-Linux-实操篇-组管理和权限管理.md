---
title: 🔒 7-Linux 实操篇 - 组管理和权限管理

date: 2025-03-02 12:00:00
categories: [Linux]
tags: [Linux, 组管理, 权限管理, 文件权限, 用户管理]
author: "kkyu9527"
cover: /images/LinuxNode/LinuxNodeCover.png
---

# 🔒 7-Linux 实操篇 - 组管理和权限管理

## 🎯 7.1 Linux 组基本介绍

📌 **组的概念**：
- 在 Linux 中，每个用户都必须属于一个组，不能独立于组外。
- 文件和目录都有 **所有者、所属组、其他用户** 三种权限控制。

📌 **查看系统中所有组**：
```bash
cat /etc/group
```

📌 **查看当前用户所属组**：
```bash
groups 用户名
```

---

## 👤 7.2 文件和目录所有者

### 📌 7.2.1 查看文件所有者
```bash
ls -ahl  # 查看所有者和权限信息
```

📌 **示例**：查看 `/home` 目录下的文件所有者
```bash
ls -ahl /home
```

### 📌 7.2.2 修改文件所有者
```bash
chown 用户名 文件名  # 修改文件所有者
```
📌 **示例**：将 `apple.txt` 的所有者更改为 `kkikikk`
```bash
chown kkikikk apple.txt
```

---

## 📂 7.3 组的管理

### 📌 7.3.1 创建新组
```bash
groupadd 组名
```
📌 **示例**：创建 `monster` 组，并创建用户 `fox` 加入该组
```bash
groupadd monster
useradd -g monster fox -m
```

### 📌 7.3.2 修改文件/目录的所属组
```bash
chgrp 组名 文件名  # 修改文件的所属组
```
📌 **示例**：将 `orange.txt` 文件的所属组修改为 `fruit`
```bash
chgrp fruit orange.txt
```

---

## 🔑 7.4 修改用户所在组

📌 **修改用户的主组**：
```bash
usermod -g 新组名 用户名
```
📌 **示例**：将 `zhangwuji` 由原来的组改为 `wudang` 组
```bash
usermod -g wudang zhangwuji
```

📌 **修改用户的附加组（保留主组）**：
```bash
usermod -aG 组名 用户名
```
📌 **示例**：将 `zhangwuji` 添加到 `shaolin` 组，但不改变主组
```bash
usermod -aG shaolin zhangwuji
```

---

## 🔍 7.5 权限的基本概念

📌 **文件权限示例**：
```bash
-rwxrw-r-- 1 root root 1213 Feb 2 09:39 abc
```
| 位数  | 含义                              |
|-----|---------------------------------|
| 0   | 文件类型 (`-` 普通文件, `d` 目录, `l` 链接) |
| 1-3 | 所有者权限 (`rwx`)                   |
| 4-6 | 组权限 (`rw-`)                     |
| 7-9 | 其他用户权限 (`r--`)                  |

📌 **权限的含义**：
- `r`（read）：可读
- `w`（write）：可写
- `x`（execute）：可执行

---

## 🛠 7.6 修改权限 (`chmod`)

### 📌 7.6.1 符号方式修改权限
```bash
chmod u=rwx,g=rx,o=x 文件名  # 设置权限
chmod o+w 文件名  # 给予其他用户写权限
chmod a-x 文件名  # 移除所有用户的执行权限
```
📌 **示例**：移除 `abc` 文件的所有者的执行权限，并增加所属组的写权限
```bash
chmod u-x,g+w abc
```

### 📌 7.6.2 数字方式修改权限
```bash
chmod 755 文件名  # 赋予 rwxr-xr-x 权限
```
📌 **示例**：
```bash
chmod 751 abc  # 拥有者 rwx, 组 rx, 其他用户 x
```

---

## 🔄 7.7 修改文件/目录所有者 (`chown`)

📌 **修改文件所有者**：
```bash
chown 新所有者 文件名
```
📌 **修改文件所有者和组**：
```bash
chown 新所有者:新组 文件名
```
📌 **递归修改目录及其中的所有文件**：
```bash
chown -R 新所有者:新组 目录名
```
📌 **示例**：
```bash
chown -R tom /home/test
```

---

## 🎯 7.8 实践 - 警察与土匪的游戏

| 组别          | 成员          |
|-------------|-------------|
| police (警察) | jack, jerry |
| bandit (土匪) | xh, xq      |

📌 **1. 创建组**
```bash
groupadd police
groupadd bandit
```

📌 **2. 创建用户**
```bash
useradd -g police jack
useradd -g police jerry
useradd -g bandit xh
useradd -g bandit xq
```

📌 **3. jack 创建文件 `jack.txt`，权限设定如下**：
```bash
touch jack.txt
chmod 640 jack.txt  # 所有者可读写，组可读，其他人无权限
```

📌 **4. 修改文件权限，允许组成员写入**
```bash
chmod g=rw,o=r jack.txt
```

📌 **5. xh 叛变加入警察组**
```bash
usermod -g police xh
```

📌 **6. 其他用户的访问测试**
```bash
su - xq  # xq 仍然无权访问
```

📌 **7. 结论**：
- **要访问目录中的文件，必须有进入目录的权限**
- `r` 权限 **仅允许查看目录内容**
- `w` 权限 **允许创建和删除文件**
- `x` 权限 **允许进入目录**

---

## 🎯 7.9 课后练习

📌 **创建两个组 (sx: 神仙, yg: 妖怪)**
```bash
groupadd sx
groupadd yg
```
📌 **创建四个用户 (唐僧, 悟空, 八戒, 沙僧)**
```bash
useradd -m tangseng
useradd -m wukong
useradd -m bajie
useradd -m shaseng
```
📌 **调整用户所属组**
```bash
usermod -g yg wukong
usermod -g yg bajie
usermod -g sx tangseng
usermod -g sx shaseng
```
📌 **悟空创建 `monkey.java` 并赋予八戒写权限**
```bash
touch monkey.java
chmod 664 monkey.java
```
📌 **八戒修改文件**
```bash
vim monkey.java
```
📌 **沙僧加入妖怪组并尝试修改文件**
```bash
usermod -g yg shaseng
vim monkey.java
```

