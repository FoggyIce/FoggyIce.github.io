---
layout:     post
title:      简约而不简单的ss服务器端搭建教程
date:       2017-09-01 15:05:43
author:     "FoggyIce"
categories:
    - 教程
tags:
    - ss
    - ss-python
    - 基于官方文档
    - 小白向
    - Ubuntu
    - 服务器
thumbnail:  https://lh5.ggpht.com/blwaF3tgja_DwoYXpozf47zI5ZiaX9RHx6atjENiwutHE9A_ZcfYUz03Y9ockvLABkntfVUiePt3HPIh7XU
---
>[题图来源][IGPJ]
>将浏览器拉窄即可看到全图
>PC版网页左上角从上到下第二个图标是目录，请多用目录
>网页右下角按钮为返回顶部，请多用返回顶部来查看顶部目录

**\[警告\]**本篇文章撰写时间较早，错漏较多，譬如战雷加速那一块的引用已经过时，请批判性阅读。

<escape><font size=4>目录</font></escape>

1. [引子](#引子)
2. [例子](#例子)
   - 2.1 [安装](#安装)
     - 2.1.1 [步骤1](#步骤1)
     - 2.1.2 [步骤2](#步骤2)
     - 2.1.3 [步骤3](#步骤3)
     - 2.1.4 [步骤4](#步骤4)
     - 2.1.5 [步骤5](#步骤5)
   - 2.2 [运行](#运行)
   - 2.3 [配合使用的实用软件(推荐但不必要)](#配合使用的实用软件-推荐但不必要)
3. [授人以鱼不如授人以渔](#授人以鱼不如授人以渔)
4. [附录](#附录)

# 引子

我也是 *身经百战，见得多了* ，哪个搭建教程我没见过？不过许多搭建教程都是 *图样图森破* ，觉得小白啥都不懂，就应该用老版本或者一键搭建脚本，用来源不明的代码仓库搭建，这样万一搭建上出了 *偏差* ，人家可是 *跑得比香港记者还快* 。

这篇教程主要就是从使用最新版本/看官方文档/用最短时间这几个角度入手来讲解如何用最少的命令和最高的 *efficiency* 来搭建ss。但并不包含如何管理vps后台，如何使用ssh远程登陆vps，系统优化，网络安全设置的部分，如果需要这些步骤的教程，请看附录贴出的我认为不错的教程，或者自行谷歌。**本教程并不鼓励任何伸手党行为，仅旨在提高谷歌搜索的信噪比**

<escape><div title="就是搜不到这种操作.jpg" align="middle"><img src="http://ww2.sinaimg.cn/mw690/61e61e8cgw1f8bk2m5xcyj20g409kq5p.jpg"></div></escape>

# 例子

## 安装

以搬瓦工ubuntu-16.04-x86_64系统在远程ssh root用户登陆下的情况为例，讲解安装ss-python分支的最新版本的方法，其中ss-python是支持AEAD加密算法的<escape><a href="#[1]">[1]</a></escape><escape><a href="#[2]">[2]</a></escape> 。以下ss-python简称ss。

```bash
apt update
apt install libsodium-dev
apt install python-pip
apt install git
pip install git+https://github.com/shadowsocks/shadowsocks.git@master
```

总共的命令数不超过5个就可以搞定ss最新版的安装，~~这就是我一直在说自己建ss非常简单的原因~~，那么现在我们一个个拆开来看看这些命令到底是干啥的。

### 步骤1

```bash
apt update
```

更新软件包列表，是每次升级系统和安装软件前所必需的。而更新软件包则是另一个指令。

### 步骤2

```bash
apt install libsodium-dev
```

Ubuntu 默认软件源里的libsodium库版本太老，不支持AEAD算法。想要使用apt命令安装ss并让ss支持AEAD算法，需要安装libsodium-dev库。
如果想自己拉github/libsodium.org上的libsodium代码编译，请自行查找支持AEAD算法的版本或者直接安装最新版，不要看到别的教程怎么说，就 *见得风是得雨*，*出现了偏差*，到时候装了一个老版本又不支持AEAD了。

### 步骤3

```bash
apt install python-pip
```

安装python包管理工具pip，方便在后面使用VCS（version control system） support功能<escape><a href="#[3]">[3]</a></escape>。

### 步骤4

```bash
apt install git
```

安装git

### 步骤5

```bash
pip install git+https://github.com/shadowsocks/shadowsocks.git@master
```

通过pip的VCS功能直接从github的代码仓库安装最新版本的ss，而非pip软件源里的老版本，这条指令在ss的github上的master分支里的readme里找到<escape><a href="#[4]">[4]</a></escape>。

## 运行

自己去看上面提到的那个readme去。

## 配合使用的实用软件(推荐但不必要)

使用supervisor托管ss并配置开机启动<escape><a href="#[5]">[5]</a></escape>。

以上。

# 授人以鱼不如授人以渔

我个人当然是推荐使用ubuntu-16.04-x86_64系统的，版本新，又有apt，小白友好型，不用管更新环境的事情（我之前就是被centos的老系统坑死了），这样基本可以直接套用以上的教程，但是每个人的环境都是不一样的，选择的服务器也是不一样的，甚至安装的版本也是不一样的，这个时候就需要自己去找解决方案。

如果某一步出现了问题，按照关键字去搜索，能直接看懂，就补装上需要的软件或者环境包。在你已经清楚要做什么的时候，首先推荐的是官方的文档，譬如安装ss-libev，我就推荐直接去看ss-libev的github的readme或者wiki。没有头绪，不清楚要干啥的时候，再去看教程，因为网上的教程通常有偏差。

针对windows下游戏的ss全局代理（包括udp转发）的教程，参见<escape><a href="#[6]">[6]</a></escape>。现在这篇简约教程就是之前那篇特殊姿势教程的精炼版本。由于那边是度娘的地盘，还请大家不要在那里回复，有什么问题在这里讨论。

# 附录

>[老高对搬瓦工后台的讲解][PHPGAOBWG]

<escape><br></escape>

<escape><a name = "[1]"><a href = "#[1]">[1]为什么要使用AEAD算法</a></a></escape>
>[为何 shadowsocks 要弃用一次性验证 (OTA)][WDSDO]

[返回安装](#安装)

<escape><br></escape>

<escape><a name = "[2]"><a href = "#[2]">[2]libsodium支持哪些AEAD算法</a></a></escape>
>[The Sodium crypto library (libsodium)][LBSDA]

[返回安装](#安装)

<escape><br></escape>

<escape><a name = "[3]"><a href = "#[3]">[3]pip的VCS support是什么</a></a></escape>
>[VCS Support][PVCS]

[返回步骤3](#步骤3)

<escape><br></escape>

<escape><a name = "[4]"><a href = "#[4]">[4]<del>隐藏分支</del></a></a></escape>
>[README.md][SSMR]

[返回步骤5](#步骤5)

<escape><br></escape>

<escape><a name = "[5]"><a href = "#[5]">[5]supervisor教程</a></a></escape>
>[使用supervisor托管shadowsocks][SSWSPVS]

[返回配合使用的实用软件](#配合使用的实用软件-推荐但不必要)

<escape><br></escape>

<escape><a name = "[6]"><a href = "#[6]">[6]贴吧OCR敏感词相关</a></a></escape>
>[使用特殊姿势给战雷加速v2.0][BDTB]

[返回授人以渔](#授人以鱼不如授人以渔)

[PHPGAOBWG]: https://blog.phpgao.com/bandwagonhost_vps_panel.html
[IGPJ]: https://www.ingress.com/intel?ll=30.507634,114.414611&z=17&pll=30.507634,114.414611
[WDSDO]: https://blessing.studio/why-do-shadowsocks-deprecate-ota/
[LBSDA]: https://jedisct1.gitbooks.io/libsodium/content/secret-key_cryptography/aead.html
[PVCS]: https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support
[SSMR]: https://github.com/shadowsocks/shadowsocks/blob/master/README.md
[SSWSPVS]: https://blog.phpgao.com/supervisor_shadowsocks.html
[BDTB]: https://tieba.baidu.com/p/5248648210