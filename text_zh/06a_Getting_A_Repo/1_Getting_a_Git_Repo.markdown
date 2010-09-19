## Getting a Git Repository ##
## 获得一个Git仓库 ##

So now that we're all set up, we need a Git repository. We can do this one of
two ways - we can *clone* one that already exists, or we can *initialize* one
either from existing files that aren't in source control yet, or from an empty
directory.

既然我们现在把一切都设置好了，我们需要一个Git仓库。有两种方法：一种是从已有的GIT仓库中clone(克隆，复制)；还有一种是新建一个仓库，把未进行版本控制的文件进行版本控制。

### Cloning a Repository ###
### Clone一个仓库 ###

In order to get a copy of a project, you will need to know the project's Git
URL - the location of the repository. Git can operate over many different
protocols, so it may begin with ssh://, http(s)://, git://, or just a username
(in which case git will assume ssh). Some repositories may be accessed over
more than one protocol. For example, the source code to Git itself can be
cloned either over the git:// protocol:

为了得一个项目的拷贝(copy),我们需要知道这个项目的地址(Git URL). Git能在许多协议下使用，所以Git url可能以ssh://, http(s)://, git://,或是只是以一个用户名（git 会认为这是一个ssh 地址）为前辍。有些仓库可以通过不同的协议来访问，例如，Git本身的源代码你可以用 git:// 协议来访问：


    git clone git://git.kernel.org/pub/scm/git/git.git

or over http:

也可以通过http 协议来访问:

    git clone http://www.kernel.org/pub/scm/git/git.git

The git:// protocol is faster and more efficient, but sometimes it is
necessary to use http when behind corporate firewalls or what have you. In
either case you should then have a new directory named 'git' that contains all
the Git source code and history - it is basically a complete copy of what was
on the server.

By default, Git will name the new directory it has checked out your cloned
code into after whatever comes directly before the '.git' in the path of the
cloned project. (ie. *git clone
http://git.kernel.org/linux/kernel/git/torvalds/linux-2.6.git* will result in
a new directory named 'linux-2.6')

### Initializing a New Repository ###
### 初始化一个新的仓库(Repository) ###
Assume you have a tarball named project.tar.gz with your initial work. You can
place it under git revision control as follows.

现在假设有一个叫”project.tar.gz”的压缩文件里包含了你的一些文件，你可以用下面的命令让它置版本控制的管理之下

    $ tar xzf project.tar.gz
    $ cd project
    $ git init

Git will reply
Git会输出:


    Initialized empty Git repository in .git/

You've now initialized the working directory--you may notice a new
directory created, named ".git".

如果你仔细观查会发现project目录下会有一个名叫”.git” 的目录被创建，这意味着一个仓库被初始化了。

[gitcast:c1_init](GitCast #1 - setup, init and cloning)
