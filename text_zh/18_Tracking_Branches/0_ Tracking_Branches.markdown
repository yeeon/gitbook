## Tracking Branches ##
## 追踪分支 ##

A 'tracking branch' in Git is a local branch that is connected to a remote
branch.  When you push and pull on that branch, it automatically pushes and
pulls to the remote branch that it is connected with.

在Git中‘追踪分支’是用与联系本地分支和远程分支. 如果你在’追踪分支'(Tracking Branches)上执行推送(push)或拉取(pull)时,　它自动推送(push)或拉取(pull)到关联的远程分支上.

Use this if you always pull from the same upstream branch into the new 
branch, and if you don't want to use "git pull <repository> <refspec>" 
explicitly.

如果你经常要从远程仓库里拉取(pull)分支到本地,并且不想很麻烦的使用"git pull <repository> <refspec>"这种格式; 那么就应当使用‘追踪分支'(Tracking Branches).


The 'git clone' command automatically sets up a 'master' branch that is
a tracking branch for 'origin/master' - the master branch on the cloned
repository.

‘git clone‘命令会自动在本地建立一个'master'分支，它是'origin/master'的‘追踪分支’. 而'origin/master'就是被克隆(clone)仓库的'master'分支.
	
译者注: origin一般是指原始仓库地址的别名.

You can create a tracking branch manually by adding the '--track' option
to the 'branch' command in Git. 

你可以在使用'git branch'命令时加上'--track'参数, 来手动创建一个'追踪分支'.

	git branch --track experimental origin/experimental

Then when you run:

当你运行下命令时:

	$ git pull experimental
	
It will automatically fetch from 'origin' and merge 'origin/experimental' 
into your local 'experimental' branch.

这会自动从‘origin'抓取(fetch)数据，再把远程的'origin/experimental'分支合并进(merge)本地的'experimental'分支.

Likewise, when you push to origin, it will push what your 'experimental' points to
to origins 'experimental', without having to specify it.

当要推送修改(push)到origin时, 它会推送你本地的'experimental'分支里修改到origin的‘experimental'分支里,　而无需指定它(origin).