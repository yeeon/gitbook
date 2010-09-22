## 建立一个公共仓库 ##

Assume your personal repository is in the directory ~/proj.  We
first create a new clone of the repository and tell git-daemon that it
is meant to be public:

假设你个人的仓库在目录 ~/proj. 我们先克隆一个新的仓库并且创建一个标志文件告诉git-daemon这是个公共仓库.

    $ git clone --bare ~/proj proj.git
    $ touch proj.git/git-daemon-export-ok

The resulting directory proj.git contains a "bare" git repository--it is
just the contents of the ".git" directory, without any files checked out
around it.

上面的命令创建了一个proj.git目录, 这个目录里有一个“裸git仓库"--只有'.git'目录里的内容,没有任何签出(checked out)的文件.

Next, copy proj.git to the server where you plan to host the
public repository.  You can use scp, rsync, or whatever is most
convenient.

下一步就是你把这个 proj.git　目录拷到你打算用来托管公共仓库的主机上. 你可以用scp, rsync或其它任何方式.

### Exporting a git repository via the git protocol ###
### 通过git协议导出git仓库 ###

This is the preferred method.

用git协议导出git仓库, 这是推荐的方法.

If someone else administers the server, they should tell you what
directory to put the repository in, and what git:// URL it will appear
at.

如果这台服务器上有管理员，TA们要行诉你把仓库放在哪一个目录中, 并且“git:// URL”除仓库目录部分外是什么.

Otherwise, all you need to do is start linkgit:git-daemon[1]; it will
listen on port 9418.  By default, it will allow access to any directory
that looks like a git directory and contains the magic file
git-daemon-export-ok.  Passing some directory paths as git-daemon
arguments will further restrict the exports to those paths.

你现在要做的是启动 linkgit:git-daemon[1]; 它会监听在 9418端口. 默认情况下它会允许你访问所有的git目录(看目录中是否有git-daemon-export-ok文件). 如果以某些目录做为 git-daemon 的参数, 那么会限制只允许用户通过git协议访问这些目录.

You can also run git-daemon as an inetd service; see the
linkgit:git-daemon[1] man page for details.  (See especially the
examples section.)

你以可以按inetd service模式运行 git-daemon; 点击 linkgit:git-daemon[1]　可以查看帮助信息.()

### Exporting a git repository via http ###
### 通过http协议导出git仓库 ###

The git protocol gives better performance and reliability, but on a
host with a web server set up, http exports may be simpler to set up.

git协议有不错的性能和可靠性, 但是如果主机上已经配好了一台web服务器,使用http协议(git over http)可能会更容易配置一些.

All you need to do is place the newly created bare git repository in
a directory that is exported by the web server, and make some
adjustments to give web clients some extra information they need:

你需要把新建的"裸仓库"放到Web服务器的可访问目录里, 同时做一些调整,以便让web客户端获得它们所需的额外信息.

    $ mv proj.git /home/you/public_html/proj.git
    $ cd proj.git
    $ git --bare update-server-info
    $ chmod a+x hooks/post-update

(For an explanation of the last two lines, see
linkgit:git-update-server-info[1] and linkgit:githooks[5].)

(最后两行命令的解释可以点击这里查看: linkgit:git-update-server-info[1] &  linkgit:githooks[5].)

Advertise the URL of proj.git.  Anybody else should then be able to
clone or pull from that URL, for example with a command line like:

拼好了proj.git的web URL, 任何人都可以从这个地址来克隆(clone)或拉取(pull)内容. 下面这个命令就是例子:

    $ git clone http://yourserver.com/~you/proj.git
