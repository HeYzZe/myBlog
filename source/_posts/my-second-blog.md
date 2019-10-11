---
title: 如何在博客中添加自己的内容
date: 2019-09-26 19:40:13
tags: [blog, hexo]
---

搭建了自己的博客之后，里面的内容就要由自己填充了。可以按照框架的模板通过md文件渲染成对应的博客页面；也可以根据自己的爱好写静态页面进行渲染。

<!-- more -->

# 简单博客页面
```javascript
  hexo new page pageName
```
以文件夹的形式新增一个博客页面，在本页面中可以继续完善自己的博客内容。
```javascript
  hexo new blog pageName
```
以md文件的形式新增一个博客页面。
```yaml
---
title: 如何在博客中添加自己的内容 // 文章的标题
date: 2019-09-26 19:40:13 // 文章的创建时间
tags: [blog, hexo] // 文章的标签
---
```
配置当前页面的一些基本参数。

# 加密博客页面
该功能需要包支持
* `npm install --save hexo-blog-encrypt`
首先在配置文件中开启插件
```yaml
encrypt:
    enable: true
```
在文章头部添加对应的字段使当前文章加密访问。
```yaml
---
category: 教程 // 类别
password: TloveY // 密码
abstract: 密码：TloveY // 摘要，显示在列表页
message:  输入密码，查看文章 // 密码框提示文字
---
```
