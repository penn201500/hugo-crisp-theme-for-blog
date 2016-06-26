+++
Categories = ["Hugo"]
Description = "如何使用hugo搭建个人博客"
Tags = ["Hugo"]
title = "如何使用hugo搭建个人博客（一）：在win7上使用hugo"
comments = true
date = 2016-06-12T19:04:40Z
+++

如何使用hugo搭建个人博客？
按照创建步骤有：
1. 在win7上使用hugo，能够本地预览（就是本文了）
2. 修改主题：颜色，字体，布局（后续）
3. 添加follow与修改share的方式（后续）
3. 添加评论系统disqus（后续）
4. 添加站内搜索（后续）
5. 放到个人vps或者推到第三方托管（推荐阅读）

Hugo 是一个用 Go 语言编写的静态网站生成器，简单易用。类似的静态网站生成器还有[Jekyll](https://jekyllrb.com/) 。

Hugo在windows 7上的使用如下：

## **1. 安装hugo**
### **1.1 安装go**
可以在go github上下载 [go 1.6](https://golang.org/dl/)
双击exe文件，一路next安装。安装完成之后，查看go安装结果：

![go](http://o7ubfyghw.bkt.clouddn.com/go_valid.jpg)

### **1.2 安装hugo**
[hugo for win64](http://download.csdn.net/detail/justheretobe/9529014)

或者官网下载：https://gohugo.io/
下载后双击exe，一路next即可。查看安装结果：
![hugo install ok](http://o7ubfyghw.bkt.clouddn.com/hugo_install_ok.jpg)


### **1.3. 安装git（用来下载主题和管理博客文件的修改信息）**
博客文件中的修改可以使用git进行版本管理，快速使用教程见: [廖雪峰 git教程]（http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000）

## **2. 创建站点**
创建一个目录，用来存放站点文件，然后使用hugo命令生成新站点：

```hugo
mkdir my_logs
hugo new site  mysite
```
运行结果：
![hugo new site mysite](http://o7ubfyghw.bkt.clouddn.com/hugo%20new%20site%20mysite.jpg)

文件结构的含义是：
原文解释见 https://gohugo.io/content/
|- archetypes           ：存放default.md，头文件格式
|- content                ：content目录存放博客文章（markdown文件）
|- data                     ：存放自定义模版，导入的toml文件（或json，yaml）
|- layouts                ：layouts目录存放的是网站的模板文件
|- static                   ：static目录存放图片，css等静态资源
|- config.toml         ：config.toml是网站的配置文件

## **3. 选择主题**
在mysite目录下新建一个themes文件夹，存放主题文件。
本例选择使用crisp主题，可以直接下载crisp主题：

```hugo
mkdir themes
cd themes
git clone https://github.com/Zenithar/hugo-theme-crisp.git
```
下载完成后：
![hugo download crisp theme](http://o7ubfyghw.bkt.clouddn.com/hugo%20download%20crisp%20theme.jpg)



## **4. 本地预览**
在cmd中启动hugo server：
hugo server --theme=hugo-theme-crisp --buildDrafts --watch

启动命令说明：
--theme 用于选择主题
--watch 用于实时监控博客文件（配置文件和博客内容）的变化，方便调试

![hugo start local server](http://o7ubfyghw.bkt.clouddn.com/hugo%20start%20local%20server.jpg)

然后在浏览器中打开 http://localhost:1313/ 
![hugo local server view](http://o7ubfyghw.bkt.clouddn.com/hugo%20local%20server.jpg)

## **5. 编写博客内容**
在content目录中创建和编写test.md：
![hugo new post test.md file](http://o7ubfyghw.bkt.clouddn.com/hugo%20new%20content-test-md%20file%20.jpg)

可以在localserver:1313中看到效果：
![localserver view test.md](http://o7ubfyghw.bkt.clouddn.com/hugo%20new%20content-test-md%20file%20view1.jpg)

打开test ：
![localserver view test.md  2](http://o7ubfyghw.bkt.clouddn.com/hugo%20new%20content-test-md%20file%20view2.jpg)


## **6. 查看更多themes以及主题Demo**
查看更多主题可以访问：
![hugo themes](http://o7ubfyghw.bkt.clouddn.com/hugo%20themes%20view--crisp.jpg)

查看crisp主题的Demo：
![huto crisp theme demo](http://o7ubfyghw.bkt.clouddn.com/crisp%20demo%20site%20with%20blogs.jpg)