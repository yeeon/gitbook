## Stashing ##
## 储藏 ##

While you are in the middle of working on something complicated, you
find an unrelated but obvious and trivial bug.  You would like to fix it
before continuing.  You can use linkgit:git-stash[1] to save the current
state of your work, and after fixing the bug (or, optionally after doing
so on a different branch and then coming back), unstash the
work-in-progress changes.

当你正在做一项复杂的工作, 这时你发现了一个和当前工作不相关但是又很讨厌的bug. 你这时想先修复bug, 那么你可以用 linkgit:git-stash[1] 来保存当前的工作状态, 当你修复完bug后,执行'反储藏‘(unstash)操作就可以回到之前的工作里.


    $ git stash "work in progress for foo feature"

This command will save your changes away to the `stash`, and
reset your working tree and the index to match the tip of your
current branch.  Then you can make your fix as usual.

上面这条命令会保你的本地修改到`储藏`(stash)中, 然后将你的工作目录和索引的内容全部重置, 回到你当前分支的上次提交时的状态. 你现在就可以开始你的修复工作了.

    ... edit and test ...
    $ git commit -a -m "blorpl: typofix"

After that, you can go back to what you were working on with
`git stash apply`:

当你修复完bug后, 你可以用`git stash apply`来回复到以前的工作状态.

    $ git stash apply


### Stash Queue ###
### 存储队列 ###

You can also use stashing to queue up stashed changes.  
If you run 'git stash list' you can see which stashes you have saved:

你也可多次使用'git stash'命令,　这样就会把‘储藏’(stash)放到一个队列中. 用'git stash list'命令可以查看你保存的'储藏'(stashes):

	$>git stash list
	stash@{0}: WIP on book: 51bea1d... fixed images
	stash@{1}: WIP on master: 9705ae6... changed the browse code to the official repo

Then you can apply them individually with 'git stash apply stash@{1}'.  You
can clear out the list with 'git stash clear'.

你可以用类似'git stash apply stash@{1}'的命令来使用任意一个'储藏'(stashes). 你可以用'git stash clear‘来清空这个队列.