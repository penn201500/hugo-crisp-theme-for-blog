+++
Categories = ["Hugo"]
Description = "如何使用hugo搭建个人博客"
Tags = ["Hugo"]
title = "如何使用hugo搭建个人博客（三）：添加follow与修改share的方式"
comments = true
date = 2016-06-06T05:04:40Z
+++

本文继续介绍如何添加follow方式与修改share的方式。

## **添加mailto的功能**
在侧边栏的follow方式中，只留下了github follow。现增加mail to 的follow方式，便于读者使用邮件方式与博主沟通。

follow方式添加mail to邮箱follow方式中也可以添加mail，图标使用fontawesome的fa fa-envelope-o。
fontqwesome的图标可以调整大小和颜色，具体讨论见：
http://stackoverflow.com/questions/12272372/how-to-style-icon-color-size-and-shadow-of-font-awesome-icons

修改  E:\github_projects\hugo-crisp-theme-for-blog\mysite\themes\crisp\layouts\partials\follow.html文件如下：

```
<div id="follow-icons">
	<a href="https://github.com/penn201500" rel="me"><i class="fa fa-github-square fa-2x"></i></a>
    <a href="mailto:penn201500@gmail.com" title="Gmail"><i class="fa fa-envelope-o fa-2x" style="color:green" style="font-size: 13px;"></i>    </a>
</div>  
```
**提醒：**请将mail地址和github地址修改为自己的帐号

显示效果：
![add mail to](http://o7ubfyghw.bkt.clouddn.com/hugo%20update%20sidebar%20add%20mailto%20follow%20method.jpg)
<p/>
<p/>
## **修改share方式**
test.md内容修改为：

```
+++
Categories = ["test"]
Description = "test"
Tags = ["test"]
menu = "main"
title = "test hugo"
comments = true
date = 2014-08-09T05:04:40Z
+++


hello hugo! I am test.md
```

默认的crisp主题在博文后面都有share方式，如红色框线部分：
![hugo post share method](http://o7ubfyghw.bkt.clouddn.com/hugo%20post%20share%20method.jpg)

如果想要删除这些share方式，可以删除header.html同目录下的share.html文件（或者注释）。删除share.html之后的显示结果为：
![hugo delete share](http://o7ubfyghw.bkt.clouddn.com/hugo%20delete%20share.jpg)<p/>
<p/>
## **删除author信息**
删除share之后，博文后面还有author信息，可以注释或删除掉header.html同目录下的author.html文件。删除author.html之后的效果为：
![hugo delete author](http://o7ubfyghw.bkt.clouddn.com/hugo%20delete%20author%20info%20after%20deleting%20share.jpg)
