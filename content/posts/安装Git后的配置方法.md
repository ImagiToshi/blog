---
title: "安装 Git 后的配置方法"
date: 2024-11-03
tags: ["Linux", "Git", "小抄"]
categories: 技术
---

~~因为自己太菜不会用 Git 所以写了个小抄~~

### 配置用户
```
git config --global user.name "username"
git config --global user.email "email@email.com"
```

然后生成 ssh 密钥：
```
ssh-keygen -t rsa -b 4096 -C "email@email.com"
```
一直按回车就行。    
在用户目录下的 `.ssh` 文件夹中找到 `id_rsa.pub` 文件，将里面的内容复制到 GitHub 添加 SSH Key 即可。

### 设置代理
不设置的话 Git 可能不走代理。
```
git config --global http.proxy 127.0.0.1:7897
git config --global https.proxy 127.0.0.1:7897
```
记得替换端口。