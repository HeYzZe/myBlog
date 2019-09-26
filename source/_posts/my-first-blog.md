---
title: 第一篇博客
date: 2019-09-25 19:40:13
tags: [hexo, GitHub, blog]
---
第一次使用[hexo]搭建自己的博客 ~ 第一篇就首先简单记录一下这篇的蛋生吧。

首先感谢[小茗同学]的博客，本次博客搭建主要是依赖于小茗大佬的博客帮助，其实他已经写的非常详细了，不过我还是记录一下我自己的搭建历程吧。

<!-- more -->

# 搭建博客的心路
其实一开始我的目的不在搭博客的，本意在于搭建服务器然后能访问外网的。后来网上浏览了不少搭建服务器的教程，想想自己的水平还没达到需要用上服务器的程度就对此冷淡了许多。![][哎]
本来到没有想搭建博客的，但是觉得还是有必要积累一些知识；闲暇之余网上浏览了一些大佬的博客教程。刚开始的时候看的是[xudailong_blog]的这篇博客，于是也就照着搭了一番，也能成功部署到了github。![][开心]
[xudailong_blog]大佬用的是GitHub + jekyll的方式搭建的博客，我看了[hexo]的主题，感觉更青睐于[hexo]；然后我就找到了[小茗同学]。
# 搭建博客的准备
对于前端搬砖的我来说，搭建博客的环境我基本都装好了（node + git + yarn/cnpm）;和我一样没有域名的话还需要在GitHub上创建一个新的库，库的名字要按照`用户名.github.io`这样的格式建；比如我的GitHub为HeYzZe，那么我就要建立一个名字为`HeYzZe.github.io`的库用来后面存放博客的代码。
# 绑定域名
有域名的话可以参照这一步将博客绑定到域名上，没有域名的也可以跳过这一步白嫖GitHub。
域名可以到`godaddy`购买或者国内阿里云也靠谱。
绑定域名分2种情况：带www和不带www的。
域名配置最常见有2种方式，CNAME和A记录，CNAME填写域名，A记录填写IP，由于不带www方式只能采用A记录，所以必须先ping一下`你的用户名.github.io`的IP，然后到你的域名DNS设置页，将A记录指向你ping出来的IP，将CNAME指向`你的用户名.github.io`，这样可以保证无论是否添加www都可以访问，如下：![][域名]
然后到你的github项目根目录新建一个名为CNAME的文件（无后缀），里面填写你的域名，加不加www看你自己喜好，因为经测试：
~~~
  * 如果你填写的是没有www的，比如 mygit.me，那么无论是访问 http://www.mygit.me 还是 http://mygit.me ，都会自动跳转到 http://mygit.me
  * 如果你填写的是带www的，比如 www.mygit.me ，那么无论是访问 http://www.mygit.me 还是 http://mygit.me ，都会自动跳转到 http://www.mygit.me
  * 如果你填写的是其它子域名，比如 abc.mygit.me，那么访问 http://abc.mygit.me 没问题，但是访问 http://mygit.me ，不会自动跳转到 http://abc.mygit.me
~~~
另外说一句，在你绑定了新域名之后，原来的`你的用户名.github.io`并没有失效，而是会自动跳转到你的新域名
# 配置SSH key
为什么要配置这个呢？因为你提交代码肯定要拥有你的github权限才可以，但是直接使用用户名和密码太不安全了，所以我们使用ssh key来解决本地和服务器的连接问题。
~~~
ssh-keygen -t rsa -C "邮件地址"
~~~
然后连续3次回车，最终会生成一个文件在用户目录下，打开用户目录，找到`.ssh\id_rsa.pub`文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key；将刚复制的内容粘贴到key那里，title随便填，保存。
# 使用hexo搭建博客
**注意：**<mark>建议统一使用git bash完成</mark>
## 安装hexo
~~~
$ npm install -g hexo
~~~
## 初始化项目
到你需要的目录下
~~~
$ npm init 文件名
~~~`
初始化完成后安装依赖
~~~
$ npm install
~~~
## 运行项目
~~~
$ hexo g // 生成
$ hexo s // 启动服务 默认端口为4000 访问localhost:4000即可
~~~
## 修改主题
官方提供了不少主题，可以挑选自己喜欢的[主题](https://hexo.io/themes/)。
我使用的主题`https://github.com/yiluyanxia/hexo-theme-antiquity.git`
挑选好主题后在themes文件夹下面：
~~~
$ git clone https://github.com/yiluyanxia/hexo-theme-antiquity.git
~~~
修改`_config.yml`中的`theme: landscape`改为`theme: yilia`，然后重新执行`hexo g`来重新生成。

如果出现一些莫名其妙的问题，可以先执行`hexo clean`来清理一下`public`的内容，然后再来重新生成和发布。

# 上传到GitHub
  首先，配置好`ssh key`;
  其次，在`_config.yml`中有关deploy的部分：
  ~~~
  deploy:
    type: git
    repository: git@github.com:HeYzZe/HeYzZe.github.io.git
    branch: master
  ~~~
  最后，安装相关依赖：
  ~~~
  $ npm install hexo-deployer-git --save
  ~~~
  安装成功后即可使用`hexo d`将你的博客打包到开始建立的代码库中
**注意：**<mark>`hexo d`使用git bash输入</mark>

到这里你的博客就已经可以通过浏览器访问了，地址为：`https://用户名.github.io/`；


<!-- 网址链接 -->
[hexo]:https://hexo.io
[小茗同学]:https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html
[xudailong_blog]:https://blog.csdn.net/xudailong_blog/article/details/78762262
<!-- 图片链接 -->
[哎]:/images/i.gif
[开心]:/images/happy.gif
[域名]:/images/20160823_191336_238_8683.png
