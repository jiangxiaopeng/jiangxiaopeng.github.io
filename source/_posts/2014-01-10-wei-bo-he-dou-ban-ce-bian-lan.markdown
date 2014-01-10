---
layout: post
title: "给blog添加豆瓣和微博侧边栏"
date: 2014-01-10 14:20:51 +0800
comments: true
categories: 
---

这篇文章介绍一下如何给blog添加豆瓣和微博的侧边栏

1.豆瓣侧边栏
首先 在 `source/_includes/post/adides` 中创建 `douban.html`,内容如下:

``` coffeescript code
<section>
<h2>我看过的</h2>
<div> </div>
</section>
```
上面代码div中的内容要在这里获取,点击[豆瓣侧边栏](http://www.douban.com/service/badgemakerjs)（记得登陆豆瓣账号）
把那段 `script` 代码粘贴过来就可以了。

2.微博侧边栏

首先 在 `source/_includes/post/adides` 中创建 `weibo.html`,内容如下:

``` coffeescript code
{% if site.weibo_user %}
<section>
  <h1>新浪微博</h1>
  <ul id="weibo">
    <li>  
    </li>
  </ul>
</section>
{% endif %}
```
li中的内容在这里获取,点击[微博侧边栏](http://weibo.com/tool/)（记得登陆微博账号）
把 `iframe` 中的代码粘贴过来。

然后在 `_config.yml` 中添加:
``` coffeescript code
# Sina Weibo
weibo_user: xxxxxxxx #user id (not user name)
weibo_verifier: xxxxxx

```
`weibo_user` 是iframe中url的uid参数的值

`weibo_verifier` 是iframe中url的verifier参数的值
