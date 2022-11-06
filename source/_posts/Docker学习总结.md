---
title: Docker学习总结
date: 2017-06-09 10:00:27
tags:
    - docker
categoroes:
    - 教程
keywords: "Docker学习总结||Docker||教学"
description: 
top_img:
cover: https://dali-saymore-public.oss-cn-shanghai.aliyuncs.com/docker.webp
---
###### **前言:**

![](http://img4.imgtn.bdimg.com/it/u=3926258919,56686921&fm=26&gp=0.jpg)

> 　最近时不时会用到很多开发工具 无奈陪伴我三年的联想y50 装了太多无用软件，这一年实习也一直用的是自己的电脑，所以不想安装太多开发软件在电脑上 所以想到了用docker容器来配置开发环境适应不同开发内容。

　docker是一个开源的容器引擎，它的观点就是服务器上安装有不同的容器 容器内配备单独的cpu和配置环境，当你需要这个环境的时候只需要单独下载容器并且使用就可以了 而且你也可以配置自己的容器，这样的办法 方便了开发人员在更换办公机器的时候为再次搭建复杂的开发环境省去了时间和麻烦，并且重启容器的时间较快只需要一秒，详细构造如下图：

![](http://upload-images.jianshu.io/upload_images/3612487-4444207933d02681.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

　我们最初的模式是a1 服务器内存放着所有的应用 但是如果其中一个应用因为内存过满导致应用崩溃那么服务器都跟着遭殃，所以需要做到应用资源独立，这时用到了a2，一台服务器上装了不同的虚拟机 每个虚拟机分配了不同的内存和cpu ，这样解决了应用资源独立问题如果应用已崩溃了 并不会影响应用2的内容，但是虚拟机启动过慢，并且如果迁移应用的时候需要从新配置虚拟机，这时候我们可以运用docker来实现第三种a3的方式，docker容器重启时间很快当应用迁移的时候，只需要把装了docker服务器镜像下载加载进去 运行就可以了。

#### 使用教程

　这里我们以服务器是Ubuntu系统为前提使用docker。

    //首先安装docker

    sudo apt-get install docker.io

    //安装完成后我们输入docker可查看详细命令参数

    docker info 命令可以帮我们查看docker的信息

　接下来我们需要的是容器现在的docker只是一个空的docker。

    //首先我们需要一个系统镜像 用 docker pull 命令获取系统镜像

    docker pull ubuntu:14.04

    // images命令可以查看本机docker中存在哪些镜像

    docker images

    // 接下来我们运行镜像 运行的镜像就叫做容器 容器可读可写 用run命令 运行镜像

    docker run -it ubuntu:14.04

    //接下来我们就进入到了容器中 所有操作并不会影响原来的系统 exit退出容器

　接下来我们将自己创建好的容器转化为镜像方便日后开发

    //ps命令可以查看我们当前都运行了哪些容器 -a参数表示运行过哪些容器

    docker ps -a

    //commit命令用来将容器转化为镜像 -m 参数用来提交说明信息 -a指定用户信息 长长的字母加数字表示容器的id 最后指定目标镜像的用户名 仓库名和tag信息

    sudo docker commit -m "xxxx" -a "xxx" id 用户名/仓库名 tag信息

    //这时我们运行 docker images 就会发现我们刚刚转化后的镜像 用docker run -it 用户名/仓库名 tag信息 我们就能运行刚刚转化后的容器

　接下来我们需要把这个刚刚创建好的容器上传到docker hub容器仓库中方便以后重复使用或者被别人使用

    //首先登陆docker hub

    docker login

    //然后我们以此输入 用户名 密码和 邮箱 最后返回login success提示

    //运行push 命令即可上传到docker hub中

    docker push 用户名/仓库名 tag信息

    //然后你就可以在docker hub中看到你上传的镜像

#### dockerfile使用

案例：利用nginx创建一个网页

　首先我们新建一个 www 目录 然后存放一个index.html文件 随便写一写些内容

　然后在www同级目录下存放一个名为dockerfle的文件并书写内容为

    FROM ubuntu:14.04 //声明构建镜像

    MAINTAINER saymagic saymagic@163.com //告诉别人你的名字和联系方式

    RUN apt-get update

    RUN apt-get install -y nginx

    COPY ./www/user/share/nginx/html //将当前系统文件拷贝到容器内目录下

    EXPOSE 80 //声明开放80端口

    CMD ["nginx","-g","daemon off;"] //表示运行容器的时候开启nginx

    //最后我们通过build来构建镜像 运行

    docker build -t="用户名/仓库名 tag信息"

　此时我们运行 docker images 就会看到刚刚生成的镜像，现在我们就可以运行刚刚的镜像了，和前面运行稍有不同，此时我们需要对外指定80端口，该行为通过-p参数指定，运行

    docker run -p 80:80 用户名/仓库名 tag信息

　此时终端会卡 因为docker思想是每个容器最好只开一个线程做一件事 现在我们可以通过localhost 查看效果

### 总结

　docker会让我们的开发变得便捷，让合作变得简单，当然还有更多docker的命令文中没有介绍，希望大家一起参考官方文档去慢慢实践练习，刚刚的例子如果不满足只在本地访问在我们没有自己服务器的前提下 利用daocloud 就可只负责写dockerfile 剩下的命令由daocloud完成。 官方传送门:[https://www.daocloud.io/](https://www.daocloud.io/)
