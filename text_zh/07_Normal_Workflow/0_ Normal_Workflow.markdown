## Normal Workflow ##
## 正常的工作流程(Normal workflow) ##

Modify some files, then add their updated contents to the index:
修改文件，将它们更新的内容添加到索引上.

    $ git add file1 file2 file3

You are now ready to commit.  You can see what is about to be committed
using linkgit:git-diff[1] with the --cached option:

你现在为commit做好了准备，你可以看看哪些文件将被提交(commit), 使用git diff命令再加上 –cached 参数。

    $ git diff --cached

(Without --cached, linkgit:git-diff[1] will show you any changes that
you've made but not yet added to the index.)  You can also get a brief
summary of the situation with linkgit:git-status[1]:

（如果没有—cached参数，git diff 会显示你所有已做的但没有加入到索引里的修改
你也可以用git status命令来获得当前项目的一个状态：

    $ git status
    # On branch master
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #	modified:   file1
    #	modified:   file2
    #	modified:   file3
    #

If you need to make any further adjustments, do so now, and then add any
newly modified content to the index.  Finally, commit your changes with:

如果你要做进一步的修改，那就继续做，做完后就把新修改的文件加入到索引中。最后把他们提交：

    $ git commit

This will again prompt you for a message describing the change, and then
record a new version of the project.

这会提示你输入本次修改的注释，完成后就会记录一个新的项目版本.

Alternatively, instead of running `git add` beforehand, you can use
除了用git add 命令，我还可以用

    $ git commit -a
    
which will automatically notice any modified (but not new) files, add
them to the index, and commit, all in one step.

这会把自动所有内容被修改的文件(不包括新加)都添加了索引中，并且同时把它们提交。

A note on commit messages: Though not required, it's a good idea to
begin the commit message with a single short (less than 50 character)
line summarizing the change, followed by a blank line and then a more
thorough description.  Tools that turn commits into email, for
example, use the first line on the Subject: line and the rest of the
commit message in the body.

这里有一个关于写commit注释的技巧和大家分享，commit注释最好以一行短句子作为开头，来简要描述一下这次commit所作的修改；然后空一行再把详细的注释写清楚。这样就可以很方便的用工具把commit释变成通知的email，第一行作为标题，剩下的部分就作email的正文。


#### Git tracks content not files ####
#### Git跟踪的是内容不是文件 ####

Many revision control systems provide an "add" command that tells the
system to start tracking changes to a new file.  Git's "add" command
does something simpler and more powerful: `git add` is used both for new
and newly modified files, and in both cases it takes a snapshot of the
given files and stages that content in the index, ready for inclusion in
the next commit.

很多版本控制系统都提供了一个“add”命令：告诉系统开始去跟踪某一个文件的改动。但是Git里的”add”命令做某些事时更简单且更强大。git add 不但是用来添加不在不在版本控制中的新文件，也用于添加已在版本控制中但是刚修改过的文件；在这两种情况下，Git都会获得当前的文件的快照并且把内容添加到索引中，为下一次commit做好准备。
[gitcast:c2_normal_workflow]("GitCast #2: Normal Workflow")