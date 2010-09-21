## The Git Index ##
## Git索引 ##

The Git index is used as a staging area between your working directory 
and your repository.  You can use the index to build up a set of changes
that you want to commit together.  When you create a commit, what is committed
is what is currently in the index, not what is in your working directory.

Git索引是一个在你的工作目录和项目仓库间的暂存区(staging area). 有了它, 你可以把许多内容的修改一起提交(commit). 如果你创建了一个提交(commit), 提交的是当前索引(index)里的内容, 而不是工作目录中的内容.

### Looking at the Index ###
### 查看索引 ###

The easiest way to see what is in the index is with the linkgit:git-status[1]
command.  When you run git status, you can see which files are staged
(currently in your index), which are modified but not yet staged, and which
are completely untracked.

用 linkgit:git-status[1] 命令是查看索引内容的最简单办法. 你运行 git status命令, 就可以看到: 哪些文件被暂存了(就是在你的Git索引中), 哪些文件被修改了但是没有暂存, 还有哪些文件没有被跟踪(untracked).

    $>git status
    # On branch master
    # Your branch is behind 'origin/master' by 11 commits, and can be fast-forwarded.
    #
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #	modified:   daemon.c
    #
    # Changed but not updated:
    #   (use "git add <file>..." to update what will be committed)
    #
    #	modified:   grep.c
    #	modified:   grep.h
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #	blametree
    #	blametree-init
    #	git-gui/git-citool

If you blow the index away entirely, you generally haven't lost any
information as long as you have the name of the tree that it described.

如果你完全掌握了索引(index), 你就一般不会丢失任何信息, 只要你记得名字描述信息(name of the tree that it described).


And with that, you should have a pretty good understanding of the basics of 
what Git is doing behind the scenes, and why it is a bit different than most
other SCM systems.  Don't worry if you don't totally understand it all right 
now; we'll revisit all of these topics in the next sections. Now we're ready 
to move on to installing, configuring and using Git.  

你最好能对Git一些基本功能运作原理, 和它与其它一些版本控制系统的区别有一个清晰的理解. 如果你在这里没有完全理解, 我们会在后面的章节重新回顾这些主题. 好的, 下面我们要去了解如何安装, 配置和使用Git.