Termux高级终端教程-05
开发环境
Termux 支持的开发环境很强，可以完美的运行 C、Python、Java、PHP、Ruby等开发环境，建议读者朋友们选择自己需要的开发环境折腾。

编辑器
写代码前总得折腾一下编辑器，毕竟磨刀不误砍柴工嘛。Termux 支持多种编辑器，完全可以满足日常使用需求。

Emacs
据说Emacs是神的编辑器，我这种小菜鸡还不会使用哎，但是 Termux 官方已经封装好了 Emacs了，我们安装起来就会简单很多:

pkg install emacs 
nano
nano 是一个小而美的编辑器。具有如下：打开多个文件，每行滚动，撤消/重做，语法着色，行编号等功能

同样安装起来也很简单：

pkg install nano
Vim
Vim 被称为编辑器之神，基本上 Linux 发行版都会自带 Vim，这个在前文基本工具已经安装了，如果你没有安装的话，可以使用如下命令安装：

pkg install vim
并且官方也已经封装了vim-python，对Python相关的优化。

pkg install vim-python
解决汉字乱码
如果你的Vim打开汉字出现乱码的话，那么在家目录(~)下,新建.vimrc文件

vim .vimrc
添加内容如下:

set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1
set enc=utf8
set fencs=utf8,gbk,gb2312,gb18030
然后source下变量:

source .vimrc
Apache
Apache是一个开源网页服务器软件，由于其跨平台和安全性，被广泛使用，是最流行的Web服务器软件之一。

安装 Apache
pkg install apache2
启动 Apache
apachectl start
然后浏览器访问: http://127.0.0.1:8080 访问是否成功启动

PS:Termux 自带的 Apache 的网站默认路径为：

$PREFIX/share/apache2/default-site/htdocs/index.html
停止 Apache
apachectl stop
重启 Apache
apachectl restart
Nginx
Nginx 是一个高性能的 Web 和反向代理服务器，Nginx 用的熟悉的话，下面搭建各种网站也就轻而易举了。

安装 Nginx
Termux 安装 Nginx 也很简单，一条命令即可：

pkg install nginx
安装完成后，我的习惯是查看一下版本信息

测试 Nginx
测试检查 Nginx 的配置文件是否正常:

nginx -t
现在测试肯定是OK的，这个多用于我们修改完 Nginx 的配置文件后的检查。

启动 Nginx
早期版本的 Termux 需要在termux-chroot 环境下才可以成功启动 Nginx ，新版本的 Termux 可以直接启动，很是方便：

nginx
Termux 在 Nginx 上默认运行的端口号是 8080， 使用pgrep命令也可以查看 Nginx 进程相关的PID号。

然后手机本地直接访问http://127.0.0.1:8080 查看 Nginx 是否正常启动

重启 Nginx
一般当修改完 Nginx 相关的配置文件时，我们需要重启 Nginx，使用如下命令即可重启:

nginx -s reload
停止 Nginx
方法一 原生停止

nginx -s stop
或者

nginx -s quit
quit 是一个优雅的关闭方式，Nginx在退出前完成已经接受的连接请求。Stop 是快速关闭，不管有没有正在处理的请求。

方法二 杀掉进程
需要1条命令，即可优雅的终止掉 Nginx 服务:

kill -9 `pgrep nginx`
貌似手机党 并不好敲 这个 ` 符号 =，= ，如果实在敲不出来，那就分两步走吧：

# 查询 nginx 进程相关的 PID 号
pgrep nginx

# 杀掉 查询出的 PID号进程
kill -9 PID
Python
Python是近几年非常流行的语言，Python 相关的书籍和资料也如雨后春笋一般不断涌现，带来了活跃了 Python 学习氛围。

安装python2
Python2 版本要淘汰了，大家简单了解一下就好：

pkg install python2 -y
安装完成后，使用python2命令启动 Python2.7 的环境

安装python3
Termux 安装 Python 默认版本是 Python3 的版本，与此同时也顺便安装了clang

pkg install python -y
安装完成后，查看下clang和Python的版本:

注意版本区分
如果你同时安装了 Python3 和 Python2 版本的话，最好向下图中这样验证一下各个版本情况，做到心知肚明，国光我是先安装 Python3 然后再安装 Python2的:

安装顺序不一样 pip 这种图片应该也就不一样
安装顺序不一样 pip 这种图片应该也就不一样

升级pip版本
pip 保持最新是一个好习惯，升级方式很简单：

Bash

升级 pip2
python2 -m pip install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple some-package

升级 pip3
python -m pip install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
这两条命令分别升级了pip2和pip3到最新版。升级完成后你会惊讶的发现你的pip3命令不见了？？？然后这个时候就开始吐槽我了

不要慌 问题不大，我们可以手动查看当前有哪些可执行的 pip 文件，使用如下命令：

ls /data/data/com.termux/files/usr/bin|grep pip
原来我们的pip3变成了pip3.8了啊
原来我们的pip3变成了pip3.8了啊
作者：小猪呐
出处：cnblogs.com/xiaozhu2020/p/Termux-05.html
