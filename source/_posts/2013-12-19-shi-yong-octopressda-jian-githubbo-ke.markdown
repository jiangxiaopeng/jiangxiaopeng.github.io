---
layout: post
title: "使用octopress搭建github博客"
date: 2013-12-19 18:26:44 +0800
comments: true
categories: 
---
{% img http://pikipity.github.io/images/post/octopress.jpg %}
### 1. 安装ruby

本地要有ruby环境，版本是1.9.3以上.

### 2. 安装octopress

我是mac os,使用git安装:

git clone git://github.com/imathis/octopress.git octopress.

然后执行:

``` coffeescript code

cd octopress

#安装依赖库
bundle install

#安装主题
bundle exec rake install

```
<!--more-->
### 3. 配置octopress

只需配置 _config.yml文件即可，设置博客的url,title,subtitle,安装第三方插件都是在这里。其中url是必须填写的，这里的url是在github上创建的一个代码仓库地址，首先需要在gitHub上创建一个仓库，并将仓库名称按照这样的方式进行命名：username.github.io，创建好仓库我们执行：

``` coffeescript code

#这条命令会帮助我们创建一个_deploy文件夹
#_deploy文件夹中的内容就是我们要提交到github代码仓库master分支的内容，其实就是我们的博客。期间会要求你输入仓库的url，根据提示，输入即可。
bundle exec rake setup_github_pages

```

接下来执行:

``` coffeescript code

#这条命令会帮助我们生成博客文件并拷贝的_deploy文件夹下
bundle exec rake generate

#这条命令会把_deploy文件夹下的内容push到远程代码仓库的master分支
bundle exec rake deploy

#如果想要在本地预览博客可以执行下面的命令, 然后浏览器输入 http://localhost:4000
bundle exec rake preview
```

把source也push到git

``` coffeescript code
git push origin source
```

现在可以访问`http://username.github.io`了。注意：有大概10分钟延迟。

到此我们的博客就搭建完了。

[github pages 官方帮助文档](https://help.github.com/categories/20/articles)

### 4. 写博客

参考：[Octopress Documentation](http://octopress.org/docs/)

写博客使用的标记语言[markdown](http://daringfireball.net/projects/markdown/basics)

### 5. 绑定自己的域名

购买域名到[godaddy](https://www.godaddy.com/)

域名绑定设置里设置两个HOST:

@ ---- `204.232.175.78`(github的ip)

`http://username.github.io`(你的github pages地址) ----- `204.232.175.78`(github的ip)

还要添加 
``` coffeescript code
echo 'your-domain.com' >> source/CNAME

git add .

git commit -m '新增CNAME文件'

git push
```
设置好之后就可以用我们自己的域名访问博客了。

### 6. 第三方的插件

我只安装了评论插件，用的是国内的[多说](http://duoshuo.com/)，比disqus访问速度快，先去多说网注册个帐号，添加站点，获取站点 short_name。

在 _config.yml 中添加:

``` coffeescript code

# duoshuo comments
duoshuo_comments: true
duoshuo_short_name: yourname
```
在 `source/_includes/post/` 中创建 `duoshuo.html`:

``` coffeescript code

<!-- Duoshuo Comment BEGIN -->
<div class="ds-thread"></div>
<script type="text/javascript">
  var duoshuoQuery = {short_name:"duoshuo_short_name"};
  (function() {
    var ds = document.createElement('script');
    ds.type = 'text/javascript';ds.async = true;
    ds.src = 'http://static.duoshuo.com/embed.js';
    ds.charset = 'UTF-8';
    (document.getElementsByTagName('head')[0] 
    || document.getElementsByTagName('body')[0]).appendChild(ds);
  })();
</script>
<!-- Duoshuo Comment END -->

```

在 `source/_layouts/post.html` 和 `source/_layouts/page.html` 中添加:

``` coffeescript code

{% if site.duoshuo_short_name and site.duoshuo_comments == true and page.comments == true %}
  <section>
    <h1>Comments</h1>
    <div id="comments" aria-live="polite">{% include post/duoshuo.html %}</div>
  </section>
{% endif %}
```

修改 `source/_includes/article.html`文件:
``` coffeescript code

 {% if site.duoshuo_short_name and page.comments != false and post.comments != false and site.duoshuo_comments == true %}
          | <a href="{% if index %}{{ root_url }}{{ post.url }}{% endif %}#comments">Comments</a>
 {% endif %}
```
完毕。

还有一些[主题大全](http://opthemes.com/)

还有很多好看的主题和好玩的插件大家自己研究吧！O(∩_∩)O哈哈~

