## Setting Up a Private Repository ##
## 建立一个私有仓库 ##

If you need to setup a private repository and want to do so locally,
rather than using a hosted solution, you have a number of options.

如果不使用第三方的代码托管服务,而是要自己在服务器上建一个私有代码仓库, 你有几种选择:

### Repo Access over SSH ###
### 通过SSH协议来访问仓库　###

Generally, the easiest solution is to simply use Git over SSH.  If users
already have ssh accounts on a machine, you can put the git repository
anywhere on the box that they have access to and let them access it over
normal ssh logins.  For example, say you have a repository you want to 
host.  You can export it as a bare repo and then scp it onto your server
like so:

通常最简单的办法是Git Over SSH. 如果你在一台机器上有了一个ssh帐号, 你只要把“git祼仓库"放到任何一个可以通过ssh访问的目录, 然后可以像ssh登录一样简单的使用它. 假设你现在有一个仓库，并且你要把它建成可以在网上可访问的私有仓库. 你可以用下面的命令, 导出一个"祼仓库", 然后用scp命令把它们拷到你的服务器上:
	
	$ git clone --bare /home/user/myrepo/.git /tmp/myrepo.git
	$ scp -r /tmp/myrepo.git myserver.com:/opt/git/myrepo.git
	
Then someone else with an ssh account on myserver.com can clone via:

如果其它人也在 myserver.com　这台服务器上有ssh帐号，　那么TA也可以从这台服务器上克隆(clone)代码:

	$ git clone myserver.com:/opt/git/myrepo.git

Which will simply prompt them for thier ssh password or use thier public key,
however they have ssh authentication setup.

上面的命令会提示你输入ssh命令公钥(public key).
译者:配置ssh公钥的方法可以参考[这里](http://help.github.com/linux-key-setup/),这样在ssh访问时就可以不要输入命令.

译者注: 你可以参考 github.com

### Multiple User Access using Gitosis ###
### Multiple User Access using Gitosis ###

If you don't want to setup seperate accounts for every user, you can use
a tool called Gitosis.  In gitosis, there is an authorized_keys file that
contains the public keys of everyone authorized to access the repository,
and then everyone uses the 'git' user to do pushes and pulls.

如果你不想为每个用户配置不同的帐号,你可以用一个叫Gitosis的工具. 在gitosis中, 有一个叫authorized_keys 的文件，里面包括了所有授权可以访问仓库的用户的公钥(public key), 这样每个用户就可以使用'git'用户来推送(push)和拉(pull)代码.

译者注: [github.com](http://help.github.com/linux-key-setup/)就是采用这种方式来配置私有(仓库)访问.

[Installing and Setting up Gitosis](http://www.urbanpuddle.com/articles/2008/07/11/installing-git-on-a-server-ubuntu-or-debian)
[安装与配置Gitosis](http://www.urbanpuddle.com/articles/2008/07/11/installing-git-on-a-server-ubuntu-or-debian)