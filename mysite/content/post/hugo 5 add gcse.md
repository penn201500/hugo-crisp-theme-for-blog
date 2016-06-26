+++
Categories = ["Hugo"]
Description = "如何使用hugo搭建个人博客"
Tags = ["Hugo"]
title = "如何使用hugo搭建个人博客（五）：添加站内搜索（gcse）"
comments = true
date = 2016-06-17T21:04:40Z
+++

站内搜索推荐使用google custom search engine(gsce)。
gcse的使用方法强烈推荐阅读：[Hexo博客优化配置之--为自己博客添加站内搜索](http://lulee007.coding.me/2016/01/23/Hexo%E5%8D%9A%E5%AE%A2%E4%BC%98%E5%8C%96%E9%85%8D%E7%BD%AE%E4%B9%8B-%E4%B8%BA%E8%87%AA%E5%B7%B1%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0%E7%AB%99%E5%86%85%E6%90%9C%E7%B4%A2/)

## **关键部分：**
![](http://o7ubfyghw.bkt.clouddn.com/hugo%20google%20search%20console.jpg)
![](http://o7ubfyghw.bkt.clouddn.com/hugo%20google%20search%20console%202.jpg)
![](http://o7ubfyghw.bkt.clouddn.com/hugo%20google%20search%20console%203.jpg)
<p/>
下面介绍如何在crisp的侧边栏中添加search box。

## **获取search.thml**
在以下github 仓库中获取search.html文件，存放到本地header.html所在的目录。
https://github.com/penn201500/hugo-crisp-theme-for-blog/blob/master/mysite/themes/crisp/layouts/partials/search.html

## **修改hearder.html：**

```
        <header id="header">
           <!--
            <a id="logo" href="{{ .Site.BaseURL }}"><img src="https://www.gravatar.com/avatar/1a2807faf3cca1667ff6f04bf5886eff.png" alt="{{ .Site.Title }}" /></a>
            -->
            <h1><a href="{{.Site.BaseURL}}">{{.Site.Title}}</a></h1>
            <p>{{.Description}}</p>

            {{ partial "follow.html" . }}
            {{ partial "navigation.html" . }}
            {{ partial "tags.html" . }}
            {{ partial "search.html" . }}     <!--这里添加search box-->       
        </header>
```

## 3. 在crisp主题下新建search文件夹
从https://github.com/penn201500/hugo-crisp-theme-for-blog/blob/master/mysite/themes/crisp/search/index.html 获取index.html放到search文件夹中。
将从google search engine中得到的搜索结果代码粘贴到index.html中的script部分：

```
    <h1 class="post-title">Search Results</h1>
    <script>
  (function() {
    var cx = '009059558632698478175:4wpqidijmx4';
    var gcse = document.createElement('script');
    gcse.type = 'text/javascript';
    gcse.async = true;
    gcse.src = 'https://cse.google.com/cse.js?cx=' + cx;
    var s = document.getElementsByTagName('script')[0];
    s.parentNode.insertBefore(gcse, s);
  })();
</script>
<gcse:searchresults-only></gcse:searchresults-only>
```
此时在侧边栏能看到search box但是不能搜索到结果:
![](http://o7ubfyghw.bkt.clouddn.com/hugo%20blog%20add%20gcse.jpg)

## 4. 生成public并发布到服务器

```
hugo -t crisp
```
在mysite目录执行以上命令，生成public目录。将public目录发布到服务器即可。
![](http://o7ubfyghw.bkt.clouddn.com/hugo%20published%20and%20can%20search%20in%20site.jpg)

如果是发布到github-pages，可以参考：
http://www.liuhaihua.cn/archives/133615.html
https://www.zhihu.com/question/20962496

---
**参考：**

[Hexo博客优化配置之--为自己博客添加站内搜索](http://lulee007.coding.me/2016/01/23/Hexo%E5%8D%9A%E5%AE%A2%E4%BC%98%E5%8C%96%E9%85%8D%E7%BD%AE%E4%B9%8B-%E4%B8%BA%E8%87%AA%E5%B7%B1%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0%E7%AB%99%E5%86%85%E6%90%9C%E7%B4%A2/)

[Hexo博客第四站：搜索引擎+小插件+配置结构分析](http://prozhuchen.github.io/2015/10/03/Hexo%E5%8D%9A%E5%AE%A2%E7%AC%AC%E5%9B%9B%E7%AB%99/)

[How do I use Google Custom Search on my website?](https://kb.iu.edu/d/bckj)