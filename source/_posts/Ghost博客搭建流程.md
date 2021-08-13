---
title: Ghost博客搭建流程
date: 2021-08-12 16:30:15
tags:
    - 博客
categoroes:
    - 教程
keywords: "如何搭建自己的博客||博客搭建"
description: 
top_img:
cover: http://wooyun.icu/ghost-alternatives.png
---

### 测试内容

###### **前言:**
![](http://upload-images.jianshu.io/upload_images/3612487-2d9f7635d9119460.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
大学实习后陆续写过一阵博客，最初只是用来记录生活一些琐事，后来慢慢的用来记录学习的记录笔记。最初的时候自己写过个人网站只不过是静态页面，那时候初学认为一个页面既可以搞定一切，后来随着学的越来越多，开始在`github`上用`hexo`搭建博客，虽说也是属于静态博客但是相比自己的页面来说那是相当方便啊，但是也一直没有坚持住写博的欲望，后来偶然从知乎看见[@罗罗磊磊](http://luolei.org)的博客，让我感受到了用博客来记录生活是件非常有趣的事情。于是在 `Vultr` 上租了2.5美元每个月云服务器，然后以`ubuntu`为基础系统搭建了现在的这个 `ghost` 博客。服务器除了搭建这个博客外也做日常翻墙使用，偶尔放几个自己写的程序跑一跑。

废话不多说，下面是搭建流程：
###### 搭建流程

准备材料：putty（连接远程云服务器），云服务器并且安卓了操作系统（本文以`Ubuntu`为例）,可解析的域名和一双能动的手。

因为ghost是需要node.js的所以首先在服务器端搭建node环境。

    //安装node.js
    sudo apt install nodejs-legacy   
    //查看node是否安装成功
    node -v    
    // 如果显示下面类似内容即成功
    v0.10.36
    //然后安装node.js的包管理工具npm
    apt-get install npm
    //查看npm是否安装成功
    npm -v    
    // 如果显示下面类似内容即成功
    v0.10.36
    //因为npm存放于国外所以可以用国内的淘宝镜像会提高下载速度
    npm install -g cnpm --registry=https://registry.npm.taobao.org
    //以后即可用cnpm命令代替npm
    //然后新建一个文件夹用来存放ghost
    sudo mkdir -p /var/www/
    //下载ghost
    sudo wget https://ghost.org/zip/ghost-latest.zip
    //解压下载的ghost文件(如果出错即是未安装unzip解压工具)
    sudo unzip -d ghost ghost-latest.zip
    //安装解压工具(上一步没出错这步忽略)
    apt-get install unzip
    //然后进入解压后的ghost文件夹并且安装生产模块
    cd ghost/
    sudo cnpm install --production
    // 到这步我们已经安装完毕ghost 剩下来我们来设置它，首先复制config.example.js文件并命名为config.js文件
    sudo cp config.example.js config.js
    //然后我们修改config.js文件的内容
    sudo nano config.js
修改为一下内容
    
    config ={
    ...
    ...
    production:{
          url:'http://你解析后的域名(如我的:laoxue.org)'
    ...
    ...
          server:{
                host:'127.0.0.1',修改这里为 '0.0.0.0'
                port:'2368'
                 }
然年后CTRL+X 在输入Y 敲回车退出编辑，现在已经配置好ghost，我们来开启ghost，观看一下。

    sudo npm start --production
    //如果是类似一下即成功
    ghost@0.6.4 start /var/www/ghost
    node index
    现在在浏览器输入 http://你的域名:2368 即可看到你的ghost。
接下来配置服务器程序去掉后面端口号

    //先安装nginx
    sudo apt-get install nginx
    //然后删除默认的文件并且编辑配置文件
    sudo rm /etc/nginx/sites-enabled/default
    sudo touch /etc/nginx/sites-available/ghost
    sudo nano /etc/nginx/sites-available/ghost

接下来是配置文件修改的内容部分
    
    server{
        listen 80;
        server_name your_domain.tld;
        location/{
             proxy_set_header  X-Real-IP $remote_addr;
             proxy)set_header  Host      $http_host;
             proxy_pass        http://你的域名:2368;
                  }
            }

然后建立一个链接，将你新建的配置告诉Nginx，并且重启nginx

    sudo ln -s /etc/nginx/sites-available/ghost /etc/nginx/sites-enabled/ghost
    sudo service nginx restart
    //接下来创建一个新用户 并且给予权限，之后会让你输入密码两次即可
    sudo adduser --shell /bin/bash --gecos 'Ghost application' ghost
    sudo chown -R ghost:ghost /var/www/ghost/

然后使用ghost用户使用系统并且开启ghost博客
   
    su - ghost
    cd /var/www/ghost
    npm start --production

之后输入域名就可以看到你的ghost博客了，然后我们让ghost保持持续运行在服务器上

    //先退出ghost 输入exit 回车
    //然后我们安装forever
    sudo npm install -g forever
    //然后执行 NODE_ENV=production forever start index.js 接下来输入
    forever list 
    //查看forever是否挂在了index.js上 然后forever index.js结束进程

到此你就可以永远的通过访问域名来访问你的ghost博客了。
你可以通过输入  http://你的域名/ghost/login  来进入ghost后台 进行写文章，修改主题等操作，因为ghost支持markdown书写方式，所以学习markdown语法会让你的文章有更好的排班。再次声明本文是给在使用ghost路上出现错误的初级用户，和一些有一点编程基础的小白，对于大神可以无视这篇文章，当然网上还有许多ghost博客搭建教程。
