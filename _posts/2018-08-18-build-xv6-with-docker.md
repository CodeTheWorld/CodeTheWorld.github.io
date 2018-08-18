---
layout: article
title: 使用docker搭建xv6环境
tags: xv6 MIT6.828
mathajx: false
---
这周为了能把xv6跑起来，尝试了各种方法，均以失败告终！

就在要放弃的时候，天佑的一句"docker"，点醒了我！

传奇就此展开！
<!--more-->

## 背景

- xv6依赖qemu运行
- centOS安装qemu各种问题

## 怎么办？

docker!!!

### 具体操作

#### 准备工作

1. 安装docker（自行查阅docker官方文档 [推荐手册](https://yeasy.gitbooks.io/docker_practice/introduction/what.html)）
2. 查找合适的搭载xv6的ubuntu镜像 [推荐xv6镜像](https://hub.docker.com/r/shqwang/xv6/)

#### 运行docker

```bash
# 下载镜像
docker pull shqwang/xv6
# 启动容器
docker run -t -i shqwang/xv6
```

这时，我们就进入ubuntu系统了。
xv6的源码目录！！！

```bash
root@f062c229465d:/# cat /etc/issue
Ubuntu 16.04 LTS \n \l

root@f062c229465d:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  xv6-public
```

#### 编译xv6

```bash
# 切换当前目录
root@9b374b994230:/# cd xv6-public/

# 编译，生成xv6.img镜像
make
-----------------------------
root@9b374b994230:/xv6-public# ls | grep xv6
xv6.img
```

#### qemu启动与退出

```bash
# 使用qemu启动xv6
qemu-system-i386 -serial mon:stdio -hdb fs.img xv6.img -smp 1 -m 512 —nographic

# 退出qemu
Ctrl+A x
```

## 参考文档

<https://hub.docker.com/r/shqwang/xv6/>

<https://www.cnblogs.com/jcli/p/4232531.html>
