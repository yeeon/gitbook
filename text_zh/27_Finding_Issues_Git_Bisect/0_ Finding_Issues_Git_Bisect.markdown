## 查找问题的利器 - Git Bisect ##

译者注:此节正在翻译中.

Suppose version 2.6.18 of your project worked, but the version at
"master" crashes.  Sometimes the best way to find the cause of such a
regression is to perform a brute-force search through the project's
history to find the particular commit that caused the problem.  The
linkgit:git-bisect[1] command can help you do this:

假设你在项目的'2.6.18'版上面工作, 但是你的"master"现在崩溃(crash)了. 有种解决这种问题这种问题的最好办法是:暴力复原(brute-force regression)项目历史,找出是哪个提交(commit)导致了这个问题. linkgit:git-bisect[1] 可以更好帮你解决这个问题:

    $ git bisect start
    $ git bisect good v2.6.18
    $ git bisect bad master
    Bisecting: 3537 revisions left to test after this
    [65934a9a028b88e83e2b0f8b36618fe503349f8e] BLOCK: Make USB storage depend on SCSI rather than selecting it [try #6]

If you run "git branch" at this point, you'll see that git has
temporarily moved you to a new branch named "bisect".  This branch
points to a commit (with commit id 65934...) that is reachable from
"master" but not from v2.6.18.  Compile and test it, and see whether
it crashes.  Assume it does crash.  Then:

如果你现在运行"git branch",你现在所在的分支是"bisect". ()
现在在这个分里,　编译并测试项目代码, 查看它是否崩溃(crash). 假设它没有出问题,那么:


    $ git bisect bad
    Bisecting: 1769 revisions left to test after this
    [7eff82c8b1511017ae605f0c99ac275a7e21b867] i2c-core: Drop useless bitmaskings

checks out an older version.  Continue like this, telling git at each
stage whether the version it gives you is good or bad, and notice
that the number of revisions left to test is cut approximately in
half each time.

现在签出一个更老的版本. 

After about 13 tests (in this case), it will output the commit id of
the guilty commit.  You can then examine the commit with
linkgit:git-show[1], find out who wrote it, and mail them your bug
report with the commit id.  Finally, run

在这个项目中, 经过13次尝试, 找出了导致问题的提交(guilty commit). 你可以用 linkgit:git-show[1] 命令查看这个提交(commit), 找出是谁做的修改，然后写邮件给TA. 最后, 运行:

    $ git bisect reset

to return you to the branch you were on before and delete the
temporary "bisect" branch.

这会到你之前(执行git bisect start之前)的状态, 并且删掉"bisect"这个临时分支.

Note that the version which git-bisect checks out for you at each
point is just a suggestion, and you're free to try a different
version if you think it would be a good idea.  For example,
occasionally you may land on a commit that broke something unrelated;
run


    $ git bisect visualize

which will run gitk and label the commit it chose with a marker that
says "bisect".  Choose a safe-looking commit nearby, note its commit
id, and check it out with:

    $ git reset --hard fb47ddb2db...

then test, run "bisect good" or "bisect bad" as appropriate, and
continue.