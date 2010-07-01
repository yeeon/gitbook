## Comparing Commits - Git Diff ##
## 比较提交 - Git Diff ##

You can generate diffs between any two versions of your project using
linkgit:git-diff[1]:

你可以用 linkegit:git-diff[1] 来比较项目中任意两个版本的差异。

    $ git diff master..test

That will produce the diff between the tips of the two branches.  If
you'd prefer to find the diff from their common ancestor to test, you
can use three dots instead of two:

上面这条命令只显示两个分支间的差异，如果你想找出‘master’,‘test’的共有
父分支和'test'分支之间的差异，你用3个‘.'来取代前面的两个'.' 。

    $ git diff master...test

linkgit:git-diff[1] is an incredibly useful tool for figuring out what has
changed between any two points in your project's history, or to see what
people are trying to introduce in new branches, etc.

### What you will commit ###
### 哪些内容会被提交(commit) ###

You will commonly use linkgit:git-diff[1] for figuring out differences between 
your last commit, your index, and your current working directory.
A common use is to simply run 

你通常用linkgit:git-diff[1]来找你当前工作目录和上次提交与本地索引间的差异。

    $ git diff
    
which will show you changes in the working directory that are not yet 
staged for the next commit. 
If you want to see what _is_ staged for the next commit, you can run

上面的命令会当前的工作目录里的，没有 staged(添加到索引中)，在提交时
不会被提交的修改。
如果你看在下次提交时要提交的内容(staged 添加到索引中),你可以运行：

    $ git diff --cached

which will show you the difference between the index and your last commit; 
what you would be committing if you run "git commit" without the "-a" option.
Lastly, you can run 

上面的命令会显示你当前的索引和上次提交间的差异；这些内容在不带"-a"参数运行
"git commit"命令时就会被提交。

    $ git diff HEAD

which shows changes in the working directory since your last commit; 
what you would be committing if you run "git commit -a".

这条命令会显示你工作目录与上次提交时之间的所有差别，这条命令所显示的
内容都会在执行"git commit -a"命令时被提交。

### More Diff Options ###
### 更多的比较选项 ###

If you want to see how your current working directory differs from the state of
the project in another branch, you can run something like

如果你要查看当前的工作目录与另外一个分支的差别，你可以用下面的命令执行:

    $ git diff test
    
This will show you what is different between your current working directory
and the snapshot on the 'test' branch.  You can also limit the comparison to a
specific file or subdirectory by adding a *path limiter*:

这会显示你当前工作目录与另外一个叫'test'分支的差别。你也以加上路径限定符，来只
比较某一个文件或目录。

    $ git diff HEAD -- ./lib 

That command will show the changes between your current working directory and
the last commit (or, more accurately, the tip of the current branch), limiting
the comparison to files in the 'lib' subdirectory.

上面这条命令会显示你当前工作目录下的lib目录与上次提交之间的差别(或者更准确的
说是当前分支)。

If you don't want to see the whole patch, you can add the '--stat' option,
which will limit the output to the files that have changed along with a little
text graph depicting how many lines changed in each file.

如果不是查看每个文件的詳細的差别，而是统计一下有哪些文件被改动，有多少行被改
动，就可以使用‘--stat' 参数。

    $>git diff --stat
     layout/book_index_template.html                    |    8 ++-
     text/05_Installing_Git/0_Source.markdown           |   14 ++++++
     text/05_Installing_Git/1_Linux.markdown            |   17 +++++++
     text/05_Installing_Git/2_Mac_104.markdown          |   11 +++++
     text/05_Installing_Git/3_Mac_105.markdown          |    8 ++++
     text/05_Installing_Git/4_Windows.markdown          |    7 +++
     .../1_Getting_a_Git_Repo.markdown                  |    7 +++-
     .../0_ Comparing_Commits_Git_Diff.markdown         |   45 +++++++++++++++++++-
     .../0_ Hosting_Git_gitweb_repoorcz_github.markdown |    4 +-
     9 files changed, 115 insertions(+), 6 deletions(-)

Sometimes that makes it easier to see overall what has changed, to jog your memory.
有时这样全局性的查看哪些文件被修改，能让你更轻轻一点。