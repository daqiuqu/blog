---
layout: post
title:  "how to build a blog by github and jekyll!"
date:   2015-01-27 10:43:35
categories: jekyll update
---

   blog终于初步可以运行了，作为第一篇正式的文章，记录一下自己blog的搭建过程。
   搭建环境：ubuntu14.04

1、环境搭建和安装

   首先安装git、ruby、gem、jekyll等，可以直接apt-get install安装：

{% highlight bash %}
apt-get install git
apt-get install ruby
apt-get install ruby-dev
apt-get install gem
{% endhighlight %}

   这时可以用 `ruby -v` 和 `gem -v` 检查一下是否安装成功，安装了什么版本。

   此时通过`gem sources list`可以查看到gem默认的源应该是`http://rubygems.org`，在中国此源速度较慢，更换为国内淘宝源，方法如下：

{% highlight bash %}
gem sources -a http://ruby.taobao.org
gem sources --remove http://rubygems.org
{% endhighlight %}

   即先添加国内源，再将默认的gem源移除，此时再用`gem sources list`查看源的设置是否正确。设置完成后安装jekyll：

{% highlight bash %}
gem install jekyll
{% endhighlight %}

   同之前一样，安装完成后用`jekyll -v`检查一下是否安装成功。

2、利用jekyll建立基本的blog

   这时安装工作基本结束，为自己的blog建立一个存放目录，`cd`到该目录之后用jekyll初始化一些基本的文件：

{% highlight bash %}
jekyll new UserName
{% endhighlight %}

   我这里出现错误`ExecJS cannot find a JavaScript runtime`，此时运行`apt-get install nodejs`安装Node.js解决该问题，安装后重新运行该命令即建立了一个以UserName命名的文件夹，里面包含一些初始化的文件。
   其中`_layout`目录用于存放模板，里面有default.html和post.html两个模板；`_post`目录用于存放博客的文章，里面有一个markdown格式的文件就是我们稍后会在网站上看到的第一篇文章；而`_post`目录下的文章会在`_site`目录下生成网页。这里还需要注意一些文件，比如`_config.yml`，其中包含了一些基本的配置选项，具体内容可以参照[Jekyll官网][jekyll-config]。其它目录和文件暂不介绍。

   实际上这时候你的个人网站已经可以在本地运行，在当前的文件夹输入：

{% highlight bash %}
jekyll serve
{% endhighlight %}

   如果之前操作没有问题的话应该可以看到`server running`字样，此时可以直接通过http://127.0.0.1:4000/本地访问自己的网站了，是不是很容易。

   现在我们开始写自己的第一个网页，如上面所说，在`_post`目录建立一个文件，命名为`yy-mm-dd-titlename.markdown`，jekyll就会根据文章的标题来创建文件夹，基本就是`/yy/mm/dd/titlename.html`的样子，我们模仿jekyll给出的例子来写第一个网页，在`_post`文件夹下新建文件`2015-01-27-hello.markdown`，内容如下：

{% highlight bash %}
---
layout: post
title: hello
---

HELLO WORLD!
{% endhighlight %}

   刷新一下本地的网页，应该就看到我们的第一篇文章了。

3、提交到github

   在本地的blog固然能给自己起到记录的作用，不过blog本来就是大家互相交流提高的地方。感谢github给我们提供了这样的方法，把blog托管到github之后，出色的版本控制也使我们不必害怕文章的丢失。
   首先在jekyll目录下运行命令:

{% highlight bash %}
git init
{% endhighlight %}

   创建一个名为gh-pages的分支：

{% highlight bash %}
git checkout --orphan gh-pages
{% endhighlight %}

   这里建立的分支名称必须是`gh-pages`，注意不要写错。

   之后就是本地提交和发布了，首先在本地提交：

{% highlight bash %}
git add .
git commit -m "Blog init"
{% endhighlight %}

   首先将当前目录加入暂存区，之后本地提交第一个版本"Blog init"是第一次提交的日志，内容可以是任何你想写的东西。

   接下来上传到github：

{% highlight bash %}
git remote add origin https://github.com/github-user-name/blog-name.git
git push origin gh-pages
{% endhighlight %}

   这样就完成了提交，访问github-user-name.github.io应该就可以查看到刚才本地调试的网页了。

   以上就是我大概的安装过程，如果有什么错误欢迎大家指出，谢谢！

   安装过程中参考了很多前人经验，包括但不限于：[蒋鑫的博客][jiangxin-blog]，[天镶的博客][tianxiang-blog]，[jekyll官网][jekyll]，[小木匠的博客][nielin-blog]，谢谢大家共享的知识和提供的工具。

[jeckyll-config]:	http://jekyllrb.com/docs/configuration/
[jiangxin-blog]:	http://www.worldhello.net/gotgithub/03-project-hosting/050-homepage.html
[tianxiang-blog]:	http://segmentfault.com/blog/skyinlayer/1190000000406011
[jekyll]:		http://jekyllrb.com/
[nielin-blog]:		http://jason1114.github.io/articles/2013/09/11/how-to-build-a-personal-homepage-with-github-pages-and-jekyll.html
