## Comparing Commits - Git Diff ##
## 比较提交 - Git Diff ##

You can generate diffs between any two versions of your project using
linkgit:git-diff[1]:

你可以用 linkegit:git-diff[1] 来比较项目中任意两个版本的差异。

    $ git diff master..test

That will produce the diff between the tips of the two branches.  If
you'd prefer to find the diff from their common ancestor to test, you
can use three dots instead of two:

这条件命令会输出个分支间的差异(diff). 如果你想看它们公有父分支...
你可用3个. 来代替2个 . 。

    $ git diff master...test

linkgit:git-diff[1] is an incredibly useful tool for figuring out what has
changed between any two points in your project's history, or to see what
people are trying to introduce in new branches, etc.

linkgit:git-diff[1] 是一个非常有用的工具，你可以用它来查看项目历史上任意
两点间的改动，或是用来查看某要加进来的新分支的情况。

### What you will commit ###
### 你将要提交的内容 ###

You will commonly use linkgit:git-diff[1] for figuring out differences between 
your last commit, your index, and your current working directory.
A common use is to simply run 
    
你通常会用 linkgit:git-diff[1]来查找你上次提交,你的的索引,你当前工作目录间的
差异。

    $ git diff
    
which will show you changes in the working directory that are not yet 
staged for the next commit. 
If you want to see what _is_ staged for the next commit, you can run

如果你要查看你项目里有哪些内容在下次提交时将要被提交，你可以执行下面的命令:

    $ git diff --cached

which will show you the difference between the index and your last commit; 
what you would be committing if you run "git commit" without the "-a" option.
Lastly, you can run 


    $ git diff HEAD

which shows changes in the working directory since your last commit; 
what you would be committing if you run "git commit -a".

### More Diff Options ###
### 更多比较参数 ###

If you want to see how your current working directory differs from the state of
the project in another branch, you can run something like

如果你要查看项目中当前分支与另一个分支之间的差异，你可以运行下面的命令:

    $ git diff test
    
This will show you what is different between your current working directory
and the snapshot on the 'test' branch.  You can also limit the comparison to a
specific file or subdirectory by adding a *path limiter*:



    $ git diff HEAD -- ./lib 

That command will show the changes between your current working directory and
the last commit (or, more accurately, the tip of the current branch), limiting
the comparison to files in the 'lib' subdirectory.

If you don't want to see the whole patch, you can add the '--stat' option,
which will limit the output to the files that have changed along with a little
text graph depicting how many lines changed in each file.

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
