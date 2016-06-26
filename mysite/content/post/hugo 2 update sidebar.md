+++
Categories = ["Hugo"]
Description = "如何使用hugo搭建个人博客"
Tags = ["Hugo"]
title = "如何使用hugo搭建个人博客（二）：修改主题：颜色，字体，布局"
comments = true
date = 2016-06-06T05:04:40Z
+++

上一篇博文中谈到了如何在本地使用hugo预览特定主题crisp，本文介绍主题的颜色，字体，布局的修改。

## **修改主题侧边栏颜色**
crisp主题的侧边栏默认是白色，如果想改个颜色咋办？
到github仓库 https://github.com/penn201500/hugo-crisp-theme-for-blog/ 获取 hugo-crisp-theme-for-blog/mysite/themes/crisp/layouts/partials/criticalpath.html  文件，替换本地themes目录下的同名文件，如
 E:\github_projects\my_blogs\mysite\themes\hugo-theme-crisp\layouts\partials\criticalpath.html
 替换之后效果：
 ![hugo update sidebar bgcolor](http://o7ubfyghw.bkt.clouddn.com/hugo%20update%20sidebar%20bgcolor.jpg)
<p/>
<p/>
## **修改主题字体**
在criticalpath.html文件中，查找font-family。然后修改字体类型，大小，颜色等
```
body,html
{
	font-size: 1em;
	line-height: 1.65em;
    font-family:"Open Sans",sans-serif;
    font-weight:300;color:#444
	background-color: #ecf0f1;
}

```


## **修改侧边栏布局**
侧边栏不想要头像？想添加links？只要github follow？ 
下面介绍如何实现这些需求

**1.去掉头像**

编辑layouts/partial目录下的header.html文件：
如：E:\github_projects\my_blogs\mysite\themes\hugo-theme-crisp\layouts\partials

```
        <header id="header">
            <a id="logo" href="{{ .Site.BaseURL }}"><img src="https://www.gravatar.com/avatar/1a2807faf3cca1667ff6f04bf5886eff.png" alt="{{ .Site.Title }}" /></a>
            <h1><a href="{{.Site.BaseURL}}">{{.Site.Title}}</a></h1>
            <p>{{.Description}}</p>

            {{ partial "follow.html" . }}
            {{ partial "navigation.html" . }}
        </header>
```
id = "logo"的这一行既是图片信息，替换图片，则将 imgsrc 连接替换。 取消图片则将这行注释或者删除。注释后效果如下：
![delete logo](http://o7ubfyghw.bkt.clouddn.com/hugo%20update%20sidebar%20delete%20logo.jpg)
<p/>
<p/>
**2. 添加links**

可以参考配置文件：https://github.com/penn201500/hugo-crisp-theme-for-blog/blob/master/mysite/themes/crisp/layouts/partials/navigation.html
将与header.html同目录的navigation.html文件修改为：

```
<hr class="nav-site-separator">
<h6>Links</h6>
<nav class="nav">
      <ul class="nav-list">
        <font size="3">
	    
		   <li class="nav-site"><a href="http://lilydjwg.is-programmer.com/" target="_blank">依云的博客</a></li>
		
		   <li class="nav-site"><a href="http://evilbinary.org/" target="_blank">邪恶二进制</a></li>
		
		   <li class="nav-site"><a href="http://www.wlman.cc/" target="_blank">Consec 's Blog</a></li>
		
		   <li class="nav-site"><a href="http://www.linuxzen.com/" target="_blank">cold's world</a></li>
		</font>
	  </ul>
</nav>
```

```<li class="nav-site"> ``` 这一行可以编辑一个链接。
修改后效果如下：
![add links](http://o7ubfyghw.bkt.clouddn.com/hugo%20update%20sidebar%20add%20links.jpg)
<p/>
<p/>
**3. 只需要github follow**

crisp主题的follow方式有facebook，twitter，linkedin，github，google+, rss 。
下面介绍如何只留github follow方式（添加或删除其他的follow方式类似）
将同目录下的follow.html修改如下：

```
<div id="follow-icons">
	<a href="https://github.com/penn201500" rel="me"><i class="fa fa-github-square fa-2x"></i></a>
</div>  
```
图标使用的是fontawesome，可以从github fork：
https://github.com/penn201500/Font-Awesome.git
或者访问fontawesome：
http://fontawesome.io/icons/

修改follow.html的效果：
![update follow method](http://o7ubfyghw.bkt.clouddn.com/hugo%20update%20sidebar%20update%20follow%20method.jpg)
<p/>
<p/>
**4.增加tags和修改title**
4.1 修改title
将E:\github_projects\my_blogs\mysite目录下的config.toml文件修改为：

```
baseurl = "http://www.learnbetter.club"
languageCode = "en-us"
title = "My Blog"
```
4.2 add tags
1.增加tags.html文件到header.html文件所在的目录。tags.html文件的内容为：

```
<h6 class="sitetaglisttitle">Tags</h6>
<ul class="sitetaglist">
    {{ range first 10 .Site.Taxonomies.tags.ByCount }}
        {{ if ge .Count 1 }}
            <li><a href="/tags/{{ .Name | urlize }}">{{ .Name }} ({{ .Count }})</a></li>
        {{ end }}
    {{ end }}
</ul>
```
2.并修改header.html：

```
        <header id="header">
           <!--
            <a id="logo" href="{{ .Site.BaseURL }}"><img src="https://www.gravatar.com/avatar/1a2807faf3cca1667ff6f04bf5886eff.png" alt="{{ .Site.Title }}" /></a>
            -->
            <h1><a href="{{.Site.BaseURL}}">{{.Site.Title}}</a></h1>
            <p>{{.Description}}</p>

            {{ partial "follow.html" . }}
            {{ partial "navigation.html" . }}
            {{ partial "tags.html" . }}  <!--增加tags-->
        </header>
```
3.修改E:\github_projects\my_blogs\mysite\content\content\test.md文件为：

```
+++
date = "2016-05-29T23:56:41+08:00"
draft = true
title = "test"
tags = "test"
+++

hello hugo! I am test.md
```
显示效果为：
![add tags and update title](http://o7ubfyghw.bkt.clouddn.com/hugo%20update%20sidebar%20update%20title%20add%20tags.jpg)

***
**注：**如果有其他好的博客主题，且托管在github上，可以clone到本地进行修改尝试