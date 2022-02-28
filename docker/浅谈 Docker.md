![浅谈 Docker](https://upload-images.jianshu.io/upload_images/4520212-1d3ab0aec60602f0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 虚拟化技术
> 虚拟化技术是一种将计算机物理资源进行抽象、转换为虚拟的计算机资源提供给程序使用的技术。

计算机资源包括
- 运算控制资源
- 数据存储资源
- 网络传输资源
- ...

![计算机资源](https://upload-images.jianshu.io/upload_images/4520212-42aed49165c57ae3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

***


**虚拟化技术为跨平台兼容而生**

![服务器分类](https://upload-images.jianshu.io/upload_images/4520212-8e72c5a18f8925bc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 实现跨平台则需要操作系统或物理硬件提供给软件层面提供统一的调用方式，程序只需要针对这套统一的接口开发即可，不需要针对不同的平台兼容不同的接口。虚拟化技术正是适配不同平台，并抽象出统一的接口提供给程序使用。

![虚拟机结构](https://upload-images.jianshu.io/upload_images/4520212-8dd8223955076a4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

***

**资源管理**

> 通过虚拟化管理计算机，可以更加灵活的控制计算机资源，还可以大幅提高计算机资源的使用率

- 控制计算机资源指不管物理机的真实资源是多少，通过虚拟化给程序传递用户规定的虚假值，程序根据给定的值处理逻辑，可以防止过度占用资源。
- 提高计算机资源的使用率，是指将被分配到某个程序但又未被使用的资源给更需要资源的程序使用，让计算机资源不被浪费，并非减少该程序的资源占用。

#### 容器技术

![容器技术](https://upload-images.jianshu.io/upload_images/4520212-69fcc0f2baa670e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


虚拟化技术
- 虚拟机（hypervisor） 如 vmware、virtualbox
- 容器（Linux Container） 如 Docker

**虚拟机**
> 虚拟机通常来说，是通过一个虚拟机监视器的设施（hypervisor），来隔离操作系统与硬件或应用程序与操作系统，来达到虚拟化的目的。

![虚拟机运行原理](https://upload-images.jianshu.io/upload_images/4520212-bc7b4886d026d1e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



在容器技术出现之前，虚拟机是业界网红，大家认为这种虚拟化可以最大程度上的提供灵活的管理。随着业务越来越庞大，分离出的服务越来越多，人们发现对于 hypervisor 环境来说，每个虚拟机都要运行一个完整的操作系统以及其中安装好的大量应用程序。但是实际的生产开发环境里，我们更关注的是自己部署的应用程序，每次都需要部署一套完整的环境不仅使得生产效率很低下，还浪费着大量的计算机资源。

**容器**
> Linux Container（简称 *LCX* ）与2008年诞生，它是一种**内核轻量级的操作系统层虚拟化技术**。Linux Container 主要由 Namespace 和 Cgroup 量大机制来保证实现的。

- Namespace 对不同 container 内使用到的网络、进程等进行隔离。
- Cgroup 负责资源的管理控制，如 Cup 与内存的使用限制，进程的控制等

它的性能远超虚拟机等其他虚拟化实现，运行在容器虚拟化的应用程序，在运行效率上与真实运行在屋里平台上的程序不相上下。

![虚拟机与容器对比](https://upload-images.jianshu.io/upload_images/4520212-93d0a115df77a615.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


由于没有了虚拟操作系统和 hypervisor 这两个层次，所有在容器中的应用程序其实完全运行在宿主操作系统中，大幅减少了应用程序运行带来的额外消耗。

*容器技术的特点*
- 轻量级
- 部署快
- 易移植
- 便管理

#### [关于Docker](https://cloud.tencent.com/developer/article/1388101)

`本章内容鸣谢掘金小册`

> Docker 由 dotCloud 公司发起，于2013年3月开源，是一个由 Go 语言实现的容器引擎。

*开源后，Docker 大火，热度远超 dotCloud 的主营业务，于是 dotCloud 直接将公司名称改为 Docker Inc，专门从事 Docker 周边的生意。并将开源的 Docker 项目改名为 [Moby](
https://github.com/moby/moby)。*

**Docker 带来的便利**

随着互联网的极速发展，应用程序的功能越来越丰富，而需要迭代的速度要求也越来越高，为了实现这些目标，应用的开发逐渐趋向服务化甚至微服务化。

![服务器架构](https://upload-images.jianshu.io/upload_images/4520212-86601b96b10b1cd9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

每个应用程序都有其对应依赖的操作系统或者其他程序，而在将应用程序细分为不同的微服务或者是其他形式的微小应用模块后，解决这种依赖问题会愈发显得棘手，有的应用运行环境特别复杂，搭建过程也很容易出错。

常遇到的问题，如在开发机器上部署的环境移交到测试环境部署，在部署的过程中会出现平台不兼容，部署之后程序运行达不到预期效果，环境不同也加大了排查问题的难度。

Docker 等容器化技术就是为了抹平平台差异，实现一次配置，多平台部署，并且 Docker 实现了快速部署，开发人员在打包部署服务时，只需关心其业务代码与相关依赖。

**Docker 官方对 Docker 在工作上带来的提升做了调查研究**

![跑个分](https://upload-images.jianshu.io/upload_images/4520212-88ea7cb71498489d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


***

**Docker 的技术实现**

Docker 主要依据以下三个技术

![技术实现](https://upload-images.jianshu.io/upload_images/4520212-7b802402d5e4ec92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 命名空间 ( Namespaces ) 

> 可分为多个子系统，如 User Namespace、Net Namespace、PID Namespace、Mount Namespace ...

例如 PID Namespace 
*我们可以造就一个独立的进程运行空间，在其中进程的编号又会从 1 开始。在这个空间中运行的进程，完全感知不到外界系统中的其他进程或是其他进程命名空间中运行的进程。*

![PID Namespace](https://upload-images.jianshu.io/upload_images/4520212-6bc7917f386fa022.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 控制组 ( Control Groups ) 

资源控制组，缩写为上文提到的 `Cgroup`。主要作用是硬件层面的隔离，根据用户规定对不同的应用程序分配不同的计算机资源，防止某个应用因逻辑问题产生 BUG 过度占用资源，甚至导致宕机，影响到同一台服务器的其他服务。

![Cgroup](https://upload-images.jianshu.io/upload_images/4520212-f9039141afd44ac3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 联合文件系统 ( Union File System ) 

> 是一种能够同时挂载不同实际文件或文件夹到同一目录，形成一种联合文件结构的文件系统。

本身与虚拟化技术无太大关系，Docker 创新型的引入，用它解决虚拟环境对文件系统占用过量，实现虚拟环境快速启停等问题。

**Docker 中，提供了一种对 UnionFS 的改进实现，也就是 AUFS ( Advanced Union File System )**

![AUFS](https://upload-images.jianshu.io/upload_images/4520212-3727f0bc4743dbaf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

由于镜像层都有唯一的编码，我们就能够区分不同的镜像层并能保证它们的内容与编码是一致的，这带来了另一项好处，就是允许我们在镜像之间共享镜像层。

![文件层级](https://upload-images.jianshu.io/upload_images/4520212-fb04ee45258da4c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

AUFS 将文件的更新挂载到老的文件之上，而不去修改那些不更新的内容，这就意味着即使虚拟的文件系统被反复修改，也能保证对真实文件系统的空间占用保持一个较低水平。

***


**Docker 理念**

![Docker 架构](https://upload-images.jianshu.io/upload_images/4520212-c55531236e69c8c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

与其他虚拟化实现甚至其他容器引擎不同的是，Docker 推崇一种轻量级容器的结构，即一个应用一个容器。

在虚拟机时代，部署 nginx、mysql、nodeServer，需要建立三台虚拟机，并装上对应的操做系统，然后在每个虚拟机中分别装上 nginx 等。而在 Docker 里，只需要创建三个对应的容器，分别运行 nginx、mysql、nodeServer，而它们所在的虚拟操作系统也直接共享于宿主机的操作系统。

**Docker 与虚拟机的参数对比**

| 属性 | Docker | 虚拟机 |
| --- | --- | --- |
| 启动速度 | 秒级  | 分钟级 |
| 硬盘使用 | M级 | G级 |
| 性能 | 接近原声 | 较低 |
| 性能 | 上百个 | 几个 |

**Docker 基于当前操作系统内核，在 Windows 或 OS X 上运行时，Docker 会在宿主机上启用一个小的 Linux 发行版 Boot2Docker**

![在 windows 与 OS X 上的实现](https://upload-images.jianshu.io/upload_images/4520212-a3173c5341b5bfb1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### Dockerfile 与 DockerHub

> Dockerfile 是 Docker 中用于定义镜像自动化构建流程的配置文件，在 Dockerfile 中，包含了构建镜像过程中需要执行的命令和其他操作。通过 Dockerfile 我们可以更加清晰、明确的给定 Docker 镜像的制作过程，而由于其仅是简单、小体积的文件，在网络等其他介质中传递的速度极快，能够更快的帮助我们实现容器迁移和集群部署。

![Dockerfile](https://upload-images.jianshu.io/upload_images/4520212-fa5bee5ccad98089.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**通过 Dockerfile 进行服务部署的好处**

- Dockerfile 的体积远小于镜像包，更容易进行快速迁移和部署。
- 环境构建流程记录了 Dockerfile 中，能够直观的看到镜像构建的顺序和逻辑。
- 在修改环境搭建细节时，修改 Dockerfile 文件要比从新提交镜像来的轻松、简单。

**Dockerfile 文件例子**

```Dockerfile
FROM debian:stretch-slim
RUN groupadd -r redis && useradd -r -g redis redis
ENV GOSU_VERSION 1.10
RUN set -ex; \
        buildDeps \
        ...
RUN mkdir /data && chown redis:redis /data
VOLUME /data
WORKDIR /data
COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 6379
CMD ["redis-server"]
```

**Dockerfile 中常用的指令**

- `FROM` **指定一个镜像作为基础镜像，如：`centos:7`，如果不基于任何镜像，则可以指定值为 `scratch`，可以出现两次，用于合并镜像**
- `ENV` **声名环境变量**
- `ADD` 与 `COPY` **同为复制文件到指定目录，ADD会识别后面的值，如果目标值为链接，则会下载，目标值为压缩文件，则会对文件进行解压缩。**
- `RUN` **向控制台发送执行命令**
- `EXPOSE` **容器中暴露的端口**
- `VOLUME` **做持久化数据时指定目录建立数据卷**
- `WORKDIR` **切换到指定目录，如果没有则会创建**
- `ENTRYPOINT` 与 `CMD` **给出运行容器时执行的命令，如果两者同时出现时，`CMD` 中的内容会作为 `ENTRYPOINT` 的参数使用。**

***

[DockerHub](https://hub.docker.com/)

**DockerHub** 与 **npmjs.com** 类似，用来上传、管理、分享自己的镜像。

![Docker Hub](https://upload-images.jianshu.io/upload_images/4520212-181ea838f0d5d651.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

DockerHub 可以与 GitHub 进行联动

![关联账户](https://upload-images.jianshu.io/upload_images/4520212-888075e730d4df4a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

GitHub 中的项目

![GitHub](https://upload-images.jianshu.io/upload_images/4520212-30b9287025a0aeac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

其中包含 Dockerfile 文件

在 DockerHub 中创建镜像

![创建与 GitHub 关联的 DockerHub 仓库](https://upload-images.jianshu.io/upload_images/4520212-a2fad43989617cba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

此后每次提交 `Git`，`DockerHub` 会自动进行 `build`

#### Docker 在项目中的运用

emmmm 持续更新中...
