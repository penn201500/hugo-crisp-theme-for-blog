+++
Categories = ["Hugo"]
Description = "如何使用hugo搭建个人博客"
Tags = ["Hugo"]
title = "如何使用hugo搭建个人博客（四）：添加评论系统disqus"
comments = true
date = 2016-06-16T15:04:40Z
+++

按照官方说法，只需要在config.toml文件中加上disqus的shortname即可让博客拥有disqus评论系统的功能。但折腾许久未能成功，现提供另一种添加disqus的方式。

**1.注册disqus**
官网注册帐号 https://disqus.com/ 
使用方式可以参考 http://alfred-sun.github.io/blog/2014/12/05/github-pages/
<p/>
**2.使用disqus**
这里使用universal code的方式，将生成的code放到新文件comments.html中：

```
<div id="disqus_thread"></div>
<script>
/**
* RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
* LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables
*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL; // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');

s.src = '//wwwlearnbetterclub.disqus.com/embed.js';

s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
```

**注：**s.src请修改为自己的帐号信息
comments.html与header.html在同一个目录。

显示效果：
![hugo add disqus](http://o7ubfyghw.bkt.clouddn.com/hugo%20add%20disqus.jpg)

<p/>
**3.博文中的comments可以关闭disqus功能**
可以对某篇博文单独关闭disqus功能。如test.md

```
+++
Categories = ["test"]
Description = "test"
Tags = ["test"]
menu = "main"
title = "test hugo"
comments = false      #这里的comments取值为false，disqus则不可见
date = 2014-08-09T05:04:40Z
+++


hello hugo! I am test.md
```
comments取值为false的显示效果为：
![hugo blog comments is false and disqus no display](http://o7ubfyghw.bkt.clouddn.com/hugo%20post-s%20comments%20is%20false%20and%20no%20disqus.jpg)

---
**注：**如果使用多说评论，请参考 http://tonybai.com/2015/09/23/intro-of-gohugo/
