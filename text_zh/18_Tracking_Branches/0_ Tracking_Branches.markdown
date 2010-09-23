## Tracking Branches ##
## 追踪分支 ##

A 'tracking branch' in Git is a local branch that is connected to a remote
branch.  When you push and pull on that branch, it automatically pushes and
pulls to the remote branch that it is connected with.

在Git中‘追踪分支’是用来把本地分支和远程分支联系起来. 如果你在这种分支上推送(push)或拉取(pull),　它也自动在与关联的远程分支进行相应操作.

Use this if you always pull from the same upstream branch into the new 
branch, and if you don't want to use "git pull <repository> <refspec>" 
explicitly.



The 'git clone' command automatically sets up a 'master' branch that is
a tracking branch for 'origin/master' - the master branch on the cloned
repository.

‘git clone‘命令会自动建立一个'master'分支，它是'origin/master'的‘追踪分支’. 而'origin/master'就是被克隆(clone)仓库的'master'分支.
	
You can create a tracking branch manually by adding the '--track' option
to the 'branch' command in Git. 

你可以在使用'git branch'命令时加上'--track'参数, 来创建一个'追踪分支'.

	git branch --track experimental origin/experimental

Then when you run:

当你运行下命令时:

	$ git pull experimental
	
It will automatically fetch from 'origin' and merge 'origin/experimental' 
into your local 'experimental' branch.

这会自动从‘origin'拉取(fetch)数据，把远程的'origin/experimental'分支合并（merge)本地的'experimental'分支.

Likewise, when you push to origin, it will push what your 'experimental' points to
to origins 'experimental', without having to specify it.

当推送(push)到origin时, 它会推送你本地的'experimental'分支到origin的‘experimental'分支,而不要指定它.