---
title: Docker原理解析
date: 2020-04-22 15:19:30
tags:
  - docker
categories: 容器化
cover: true

---

## 1. 容器是什么

引用 [Docker 官网](https://www.docker.com/resources/what-container)对容器的一个定义：

> What is a Container?
>
> A standardized unit of software.

容器是什么？一个软件的**标准化单元**。

我们来分析下这个定义，首先是**软件**，跟容器相关的是软件而不是硬件，而我们也知道软件主要分为系统软件和应用软件，而容器中运行的程序并非系统软件，它实际运行在宿主机上，与宿主机上的其他进程共用一个内核，这也是容器与传统虚拟机的一个很大区别。

再者，**标准化单元**，刚才我们已经说了，容器内运行的程序并非系统软件，每个软件运行都需要有必要的环境，包括一些 lib 库之类的，而如何能在复杂的环境中做到“标准化”呢？显然，**隔离**是一个最佳选择。将程序及其所需的环境 /lib 库之类的组织在一起，并与系统环境隔离，这就很容易做到“标准化”了。

说白了，**容器其实是在一台机器上的“一组”进程，当然这组进程可能只有一个；它们有相同的特性，同样所受的限制也相同；另外既然叫做容器，很自然地我们认为它们与外界可以进行隔离/应该有一个分界线。**

如何隔离? Docker最初基于Linux Container(LXC) ,并在2014年正式发布1.0之前将LXC换成了自己实现的libcontainer,但归根结底,其实还是基于cgroups、namespace、Union File Systems等技术。

## 2. cgroups



## 3. namespace

## 4. UnionFileSystem