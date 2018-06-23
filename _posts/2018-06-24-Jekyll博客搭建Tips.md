---
layout: post
title:  "Jekyll博客搭建Tips"
description: "根据模板作者的教程搭建博客时遇到一些坑，分享在这里作为笔记，避免其他人踩到一样的坑不知道怎么解决"
tags: 博客
mermaid: true
comments: true
date: 2018/06/24 01:31:00
---

Jekyll博客搭建Tips
====

本文是根据模板作者的教程搭建博客时遇到一些坑的解决方法，不同的人搭建博客遇到的坑可能不一样，谨在此记录下我遇到的坑和总结的tips，希望能对搭建博客遇到问题的小伙伴有帮助。下面的教程大部分是原作者的教程，我会进行一些修改将遇到的问题和大致安装过程分开，便于读者查找。

----

搭建Jekyll博客教程
----

### 介绍

 　Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的

　使用 Jekyll 搭建博客之前要确认下本机环境，Git 环境（用于部署到远端）、[Ruby](http://www.ruby-lang.org/en/downloads/) 环境（Jekyll 是基于 Ruby 开发的）、包管理器 [RubyGems](http://rubygems.org/pages/download)
　　如果你是 Mac 用户，你就需要安装 Xcode 和 Command-Line Tools了。下载方式 Preferences → Downloads → Components。

　　Jekyll 是一个免费的简单静态网页生成工具，可以配合第三方服务例如： Disqus（评论）、多说(评论) 以及分享 等等扩展功能，Jekyll 可以直接部署在 Github（国外） 或 Coding（国内） 上，可以绑定自己的域名。[Jekyll中文文档](http://jekyll.bootcss.com/)、[Jekyll英文文档](https://jekyllrb.com/)、[Jekyll主题列表](http://jekyllthemes.org/)。


### Jekyll 环境配置

安装 jekyll

```
$ gem install jekyll
```

创建博客

```
$ jekyll new myBlog
```

进入博客目录

```
$ cd myBlog
```

启动本地服务

```
$ jekyll serve
```

在浏览器里输入： [http://localhost:4000](http://localhost:4000)，就可以看到你的博客效果了。

![](/images/posts/jekyll/image1.png)

so easy !

### 目录结构
　
　Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是： 你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile,或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

 一个基本的 Jekyll 网站的目录结构一般是像这样的：

```
.
├── _config.yml
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   ├── post.html
|   └── page.html
├── _posts
|   └── 2016-10-08-welcome-to-jekyll.markdown
├── _sass
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md
├── css
|   └── main.scss
├── feed.xml
└── index.html

```

这些目录结构以及具体的作用可以参考 [官网文档](http://jekyll.com.cn/docs/structure/)

进入 _config.yml 里面，修改成你想看到的信息，重新 jekyll server ，刷新浏览器就可以看到你刚刚修改的信息了。

到此，博客初步搭建算是完成了，

### 博客部署到远端

　我这里讲的是部署到 Github Page 创建一个 github 账号，然后创建一个跟你账户名一样的仓库，如我的 github 账户名叫 [leopardpan](https://github.com/leopardpan)，我的 github 仓库名就叫 [leopardpan.github.io](https://github.com/leopardpan/leopardpan.github.io)，创建好了之后，把刚才建立的 myBlog 项目 push 到 username.github.io仓库里去（username指的是你的github用户名），检查你远端仓库已经跟你本地 myBlog 同步了，然后你在浏览器里输入 username.github.io ，就可以访问你的博客了。


### 编写文章

　　所有的文章都是 _posts 目录下面，文章格式为 mardown 格式，文章文件名可以是 .mardown 或者 .md。

　　编写一篇新文章很简单，你可以直接从 _posts/ 目录下复制一份出来 `2016-10-16-welcome-to-jekyll副本.markdown` ，修改名字为 2016-10-16-article1.markdown ，注意：文章名的格式前面必须为 2016-10-16- ，日期可以修改，但必须为 年-月-日- 格式，后面的 article1 是整个文章的连接 URL，如果文章名为中文，那么文章的连接URL就会变成这样的：http://baixin.io/2015/08/%E6%90%AD%E5/ ， 所以建议文章名最好是英文的或者阿拉伯数字。 双击 2016-10-16-article1.markdown 打开

```

---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-10-16 11:29:08 +0800
categories: jekyll update
---

正文...

```


title: 显示的文章名， 如：title: 我的第一篇文章
date:  显示的文章发布日期，如：date: 2016-10-16
categories: tag标签的分类，如：categories: 随笔

注意：文章头部格式必须为上面的，.... 就是文章的正文内容。

我写文章使用的是 Atom 编辑器，如果你对 markdown 语法不熟悉的话，可以看看[作业部落的教程](https://www.zybuluo.com/)


### 使用我的博客模板

虽然博客部署完成了，你会发现博客太简单不是你想要的，如果你喜欢我的模板的话，可以使用我的模板。

首先你要获取的我博客，[Github项目地址](https://github.com/leopardpan/leopardpan.github.io.git)，你可以直接[点击下载博客](https://github.com/leopardpan/leopardpan.github.io/archive/master.zip)，进去leopardpan.github.io/ 目录下， 使用命令部署本地服务

```
$ jekyll server
```

当提示

```
Configuration file: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_config.yml
            Source: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github
       Destination: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.901 seconds.
 Auto-regeneration: enabled for '/Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github'
Configuration file: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

```

表示本地服务部署成功。

在浏览器输入 [127.0.0.1:4000](127.0.0.1:4000) ， 就可以看到[DateBro's Blog](https://datebro.github.io/)博客效果了。

### 修改成你自己的博客

>* 如果你想使用我的模板请把 _posts/ 目录下的文章都去掉。
>* 修改 _config.yml 文件里面的内容为你自己的。

然后使用 git push 到你自己的仓库里面去，检查你远端仓库，在浏览器输入 username.github.io 就会发现，你有一个漂亮的主题模板了。


### 为什么要是用 Jekyll

使用了 Jekyll 你会发现如果你想使用多台电脑发博客都很方便，只要把远端 github 仓库里的博客 clone 下来，写文章后再提交就可以了，Hexo 由于远端提交的是静态网页，所有无法直接写 Markdown 的文章。

----

### 拓展博客功能，添加 *评论* 功能

这个可以参考 [*我搭建过程中参考的博客*](https://booox.github.io/2017/04/22/add-disqus-to-jekyll/)

----

遇到的坑和解决办法
----

### 安装ruby后命令出错

例如:
> gem不是内部程序

之类的错误

原因：
> 安装ruby时没有修改环境变量

解决方法：
> 将ruby安装文件夹下bin目录加入path环境变量即可

----

### *尝试本地预览作者博客模板时报错*

如果你本机没配置过任何jekyll的环境，可能会报错

```
/Users/xxxxxxxx/.rvm/rubies/ruby-2.2.2/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require': cannot load such file -- bundler (LoadError)
	from /Users/xxxxxxxx/.rvm/rubies/ruby-2.2.2/lib/ruby/site_ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/gems/jekyll-3.3.0/lib/jekyll/plugin_manager.rb:34:in `require_from_bundler'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/gems/jekyll-3.3.0/exe/jekyll:9:in `<top (required)>'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/jekyll:23:in `load'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/jekyll:23:in `<main>'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/ruby_executable_hooks:15:in `eval'
	from /Users/xxxxxxxx/.rvm/gems/ruby-2.2.2/bin/ruby_executable_hooks:15:in `<main>'

```

原因： 没有安装 bundler
>解决方法：执行安装 bundler 命令

```

$ gem install bundler

```


提示：

```
Fetching: bundler-1.13.5.gem (100%)
Successfully installed bundler-1.13.5
Parsing documentation for bundler-1.13.5
Installing ri documentation for bundler-1.13.5
Done installing documentation for bundler after 5 seconds
1 gem installed

```

再次执行 $ jekyll server  ，提示

```

Could not find proper version of jekyll (3.1.1) in any of the sources
Run `bundle install` to install missing gems.

```

跟着提示运行命令

```
$ bundle install
```

这个时候你可能会发现 bundle install 运行卡主不动了。

如果很长时间都没任何提示的话，你可以尝试修改 gem 的 source

```
$ gem sources --remove https://rubygems.org/
$ gem sources -a http://ruby.taobao.org/
$ gem sources -l
*** CURRENT SOURCES ***

http://ruby.taobao.org

```

再次执行命令 $ bundle install，发现开始有动静了

```
Fetching gem metadata from https://rubygems.org/...........
Fetching version metadata from https://rubygems.org/..
Fetching dependency metadata from https://rubygems.org/.
。。。
Installing jekyll-watch 1.3.1
Installing jekyll 3.1.1
Bundle complete! 3 Gemfile dependencies, 17 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.

```

bundler安装完成，后再次启动本地服务

----

### *再次启动本地服务时报错*

```
$ jekyll server

```

继续报错

```
Configuration file: /Users/tendcloud-Caroline/Desktop/leopardpan.github.io/_config.yml
  Dependency Error: Yikes! It looks like you don't have jekyll-sitemap or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-sitemap' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!
jekyll 3.1.1 | Error:  jekyll-sitemap

```
表示 当前的 jekyll 版本是 3.1.1 ，无法使用 jekyll-sitemap

解决方法有两个

> 1、打开当前目录下的 _config.yml 文件，把 gems: [jekyll-paginate,jekyll-sitemap] 换成 gems: [jekyll-paginate] ，也就是去掉jekyll-sitemap。

> 2、升级 jekyll 版本，我当前的是 jekyll 3.1.2 。

修改完成后保存配置，再次执行

```
$ jekyll server

```

----

### *再次启动本地服务时报错，且与上次错误不同*

例如：
```

block in materialize': Could not find ffi-1.9.18 in any of the sources (Bundler::GemNotFound) from D:/rubyInstall/Ruby25-x64/lib/ruby/gems/2.5.0/gems/bundler-1.16.1/l ib/bundler/spec_set.rb:82:inmap!'

```

原因：
>这个错误的重点在`Could not find ffi-1.9.18`，使用`gem list`查看你安装的ffi版本，应该不是1.9.18版本。而且因为作者的配置文件中安装包的版本可能不止一个不对，所以下次 `jekyll server`后仍可能报某个安装包版本不对的错 所以要一个一个解决，直到不报错为止。

解决办法：
> 打开目录下的`Gemfile.lock`文件，对照`gem lis`列出的相应安装包，找到并修改对应的版本号，修改为你电脑安装的版本就可以了。

----

### 奇怪的Dependency Error

报错信息：
> Dependency Error: Yikes! It looks like you don't have /Users/rpa/Sites/jekyll/rabernat.github.io/_plugins/ext.rb or one of its dependencies installed.
>In order to use Jekyll as currently configured, you'll need to install this gem.
>The full error message from Ruby is: 'cannot load such file -- jekyll/scholar'
>If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!
>jekyll 3.1.6 | Error:  /Users/rpa/Sites/jekyll/rabernat.github.io/_plugins/ext.rb

解决方法：
> 把Gemfile.lock删除重新本地加载一次即可

----

### *同步到GitHub上时GitHub发邮件警告*

邮件报警告：The CNAME `baixin.io` is already taken
> 解决：把CNAME里面的baixin.io修改成你自己的域名，如果你暂时没有域名，CNAME里面就什么都不用谢。（之前没人反馈过这个问题，应该是github page最近才最的限制。）

----

### 本地同步到GitHub时无法正常同步，出现 *fatal: AggregateException encountered.*

原因：
> 这是Git版本过低导致的

解决方法：
> 升级Git即可，不过Windows上升级Git只能重新下载更高级版本的安装包。[Git下载地址](https://git-scm.com/download)

----

### 以上完成后本地文件夹中多出index.md文件导致无法预览

原因：
> index.md文件中可能有些配置和模板不符，删除即可

解决方法：
> 删除index.md文件

----

### 通过Disqus服务添加评论功能后预览无法显示

原因(这个仅供参考)：
> 电脑暂时无法FQ，可能用于FQ的代理IP被封或者校园网这段时间不稳定，无法正常显示

解决方法：
> 过一段时间再预览，可以尝试登陆Disqus查看是否已经无法FQ

----

### 我遇到的坑主要就是这些，希望能对大家有所帮助.

----

### *如果你在搭建博客遇到问题，可以在评论里给我提问。*
