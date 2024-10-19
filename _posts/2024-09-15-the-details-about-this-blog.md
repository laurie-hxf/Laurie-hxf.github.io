---
layout: post
title: the details about this blog
date: 2024-09-15 20:22:00 +0800
description: the details about this blog
tags: 其他
categories: sample-posts
---
本博客基于github pages中的al-folio为主题

就记录一下配置这篇博客的细节 以便以后需要重新配置之后可以节约时间

主题网站：https://github.com/alshedivat/al-folio 

样例：https://alshedivat.github.io/al-folio/

安装该主题：https://github.com/alshedivat/al-folio/blob/master/INSTALL.md （最开始配置可以看里面的视频）

修改该主题：https://github.com/alshedivat/al-folio/blob/master/CUSTOMIZE.md

giscus评论：https://giscus.app/zh-CN

git pages: https://pages.github.com

jekll官网 :https://jekyllrb.com （里面有各种主题）


温馨提示：当每次修改本地仓库的内容后，将它push到远程仓库，一般要等待几分钟，不用额外对github进行操作，最好在你要改变一些东西的时候连同改变一些像news的内容，这样你就可以判断你要改的东西有没有成功部署
最后善用gpt 一切不懂的都可以问他
以及千万不能在这个blog文件夹中新建文件夹，否则不知道会出什么混乱
以及每次写完一篇博客或news的时候，一定要注意那里的时间是不是当前的时间，如果是以后的时间，他有可能要等到那个时间才会展现出来。

### 编写
这篇博客有一个本地仓库，通过本地git仓库与github仓库远程连接，然后通过vscode进行本地编写


### 评论
本博客的评论是基于主题自带的评论，（位于_config.yml文件中Giscus comments），配置教程[这个](https://giscus.app/)首先创建一个public的仓库用来存储评论，并且在setting中设置允许discussion功能，具体可看官网教程。当填写仓库和discussion选项之后会在下面生成一段代码，然后将_config文件根据生成代码填写。之后有一步很重要的操作就是将那段代码复制粘贴到_layouts/default.liquid文件最下面（记住要放在<body>中）原因就是要在default中再生成一个新区间，才能反应到前段中。


### 主页
主页中的内容一部分是在_pages/about.md中修改（包括自我陈述，图片下面的文字），还有一部分是在_config.yml中修改（包括名字的修改），头像的话在assets/img中将想要展现的头像重命名为prof_pic.jpg


### news
在_news中添加文件，格式的话最简单就是在之前的文件里更改或者按照之前的文件进行更改

new文件夹最多只能有4个announcements否则会出现问题

### 子目录
子目录的管理在_pages文件夹中，原本的样例网站中有很多个子目录，可以选择是否显示这些目录


##### blog
这个子目录下的最上层文字在_config.yml文件blog那里编辑，包括下面的tag，可以添加tag选项，然后要写blog的话就在_post文件夹中增加文件，文件名格式为year-month-day-blogname.md，然后具体写博客的话可以参考原本的模版进行修改，同时可以对每篇博客添加tag以便进行分类查找。


##### repositories
这个在_data/repositories中配置


##### cv
具体的cv内容可以从_data/cv.yml中进行修改，参考[主题网站](https://github.com/alshedivat/al-folio/blob/master/CUSTOMIZE.md)中有提到怎么修改