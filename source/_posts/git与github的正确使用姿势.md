---
title: git与github的正确使用姿势
date: 2017-08-13 11:37:48
tags:
    - git
categoroes:
    - 工具
keywords: "git与github的正确使用姿势||git||github"
description: 
top_img:
cover: https://edupala.com/wp-content/uploads/2018/05/git.png
---

![github](http://upload-images.jianshu.io/upload_images/3612487-278319f5ac3cd441.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### git与github 

在学习如何使用git和github前我们先详细了解下什么是git？而github又是什么？

git是一种分布式版本控制系统，他可以记录你开发过程中的每一次改动，也就是记录你每次改变的版本，可以进行回退，在版本间自由切换。而且git是分布式的也就说更利于团队间的合作，你发布你的版本后，如果有其他成员想对它进项更改，只需要git clone你的版本 改动后在push下 如果你感觉他的改动符合你的想法只需要 合并就可以形成新的版本了。

而github就是一个开源的社区，使用git来进行操作。github就像是一个大仓库，储存了很多优秀的开源代码，也有人戏称github是最大的 “同性交友社区”。

在了解了git与github后我们就来看一看如何进行操作吧。（以下例子是已经下载git 并且配置环境变量的前提下）

比如我完成了我的项目，以后可能会进行更改，但是我又怕改动后找不到原来的版本了这时候我就觉得我该使用git了。  

我的仓库名字叫做 “demo”，这时候我需要在命令行输出 cd demo 切换到demo目录下：

然后 git init 代表我初始化了这个项目 要使用git对其进行操作

再然后 使用 git add * 代表我把这个项目所有文件都存到了git的暂存区中

之后 git commit -m “版本一” 这句代表我这次的提交说明，代表我这次提交的是项目的版本一

这个时候如果你暂时不打算使用github，基本就告一段落了，git已经把你的项目复制到一个隐藏的文件夹内并且给她设置了一个名为版本一的信息。

这个时候你突然想继续更改你的项目，只需要直接更改。 更改过后你想把这次的更改提交为版本二 这个时候 使用 git status 就可以查看你这次跟上次相比改动的部分，然后依旧 git add * 也可以只提交你改动的文件 * 代表所有文件。 之后git commit -m “版本二” 代表第二次提交的名称为版本二。

你发布版本二后发现这个版本并不是你想要的你想从版本一重新开始编辑 这个时候我们使用 git log 可以查看每次提交的git 历史记录 我们可以看到有 版本一 版本二两个版本，使用 git reset --hard HEAD^ 这个时候我们打开项目发现我们的项目代码退回到了版本一的样子。

git reset --hard commit_id 这个命令就是让git回退到指定版本 使用git reflog可以查看每次版本的 commit_id ，之后使用命令就可切换到对应版本。

现在我们想把我们的项目发布到github中：（下面例子在你已经注册了github的前提下进行）

生成ssh-key ： ssh-keygen -t rsa -c "user-email" 

然后 cat ~/.ssh/id_rsa.pub  查看刚刚创建的ssh-key 复制它
如果命令无效 你就在你的盘中找id_rsa.pub文件复制里面的内容。

在github中有个ssh设置 把你复制的内容粘贴到上面。

然后输入 ss -T git@github.com 查看是否连接github成功。

如果回车看到：You’ve successfully authenticated, but GitHub does not provide shell access 。表示已成功连上github。

首先让git与github创建一个连接：

git config --global user.name 设置你的github名字到git配置文件中
git config --global user.email 设置你的github邮箱到你的git配置文件中

然后在github中创建一个库用来装你本地的项目，创建成功后 会有一个库的地址记录下来

git remote add origin git@github.com:yourName/yourRepo.git 把后面的部分改成你的仓库地址 代表将你的项目与github库连接

接下来使用 git push origin master 代表将你的本地项目上传到github中 master代表上传到主分支 如果传到其他分支则需要更改为其他分支名字。

如果本地更改依旧执行上述 git add 和 git commit 命令 然后git push 上传，github就会更新你的项目。

这里有个注意点，就是如果你在github中更改了文件，本地是不会有改动的，这个时候如果你改动了本地在push 就会有错误。  你先使用git pull 更新本地库 然后 git merge <branch> 尝试自动合并你的改动 之后再push 就可以了。

### 最后

其实还有如git checkout 、git branch等命令我没有详细的讲，因为涉及太多我这里只是讲一个大概的git与github的流程，让大家对git和github有个简单的了解。 如果大家想详细的学习git我推荐下廖雪峰老师的git教学，百度就可以搜到，很详细并且有许多的配图能形象的了解git的原理，我的文章中如果有哪些错误也请大家指正，我会加以修改。

最后也希望我能坚持住无聊时写一些文章的习惯吧，我的个人博客也会同步更新文章。
