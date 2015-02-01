---
layout: post
title:  "利用vundle管理vim插件!"
date:   2015-01-31 08:39:19
categories: vundle vim swift
---

想用vim来看swift代码，但是没有swift语法高亮，查了下可以用插件解决，而vim下管理插件的神器要数vundle了，vundle也就是vim bundle。
方法其实很简单，如果没有git的话首先安装git，`apt-get install git`。

1、安装完成后从github上下载vundle：

{% highlight bash %}
git clone http://github.com/gmarik/vundle.git ~/.vim/bundle/vundle
{% endhighlight %}

2、接下来主要是配置.vimrc，从vundle的README.md可以看到需要的修改，修改后运行vim的时候就会首先加载.vimrc中的配置，不明白怎么配置的话可以先参考别人的，比如我参考了beiyuu的[vimrc][beiyuuVimrc]。

3、之后运行vim，执行:BundleInstall就可以安装.vimrc里规定的插件。

vundle提供了以下几种插件安装方法：

  如果这是一个在github的repository的话，比如我安装的swift语法高亮插件，采用这种形式：`Bundle "toyamarinyon/vim-swift"`，这个插件应该是目前github上同类型里starred最多的。

  如果是一个git插件，但是没有托管在github，采用这种形式：`Bundle 'git://git.wincent.com/command-t.git'`。

  如果是一个本地的git插件，采用这种形式：`Bundle file:///home/gmarik/path/to/plugin`。


vundle共提供了这几个命令：

  BundleInstall：安装插件

  BundleList:当前插件列表

  BundleClean:卸载不在列表中的插件

  BundleInstall！：更新插件

运用这几个命令，就可以轻松的利用vundle管理vim插件了，插件都存放在`~/.vim/bundle/`目录下。

主要参考了vundle readme和beiyuu的vimrc，谢谢贡献！

[beiyuuVimrc]:  https://github.com/beiyuu/vimfiles/blob/master/_vimrc
