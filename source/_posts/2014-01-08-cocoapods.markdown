---
layout: post
title: "IOS 包管理工具 CocoaPods"
date: 2014-01-08 11:32:16 +0800
comments: true
categories: 
---


这次介绍一款ios的 包管理工具 CocoaPods，类似rubygem，我试用了一下还不错，附上使用方法：

1.要安装ruby和rubygem,我本地ruby版本是2.0.0-p247，gem版本2.0.6

2.安装CocoaPods:

``` coffeescript code
gem install cocoapads

pod setup 

```

3.使用CocoaPods:
进入到你的ios项目根目录，然后创建一个名为Podfile的文件,文件内容如下

``` coffeescript code
platform :ios ,'7.0' #版本
pod 'AFNetworking' , '~> 2.0.3'  #需要使用的第三防库。

```
然后执行

``` coffeescript code
pod install

```

4.运行项目要运行项目路径下的project_name.xcworkspace文件。

