## Maintaining Git ##
## 维护Git ##

### Ensuring good performance ###
### 保证良好的性能 ###

On large repositories, git depends on compression to keep the history
information from taking up too much space on disk or in memory.

在大的仓库中, git靠压缩历史信息来节约硬盘和内存空间.

This compression is not performed automatically.  Therefore you
should occasionally run linkgit:git-gc[1]:

压缩操作并不是自动进行的, 你手动执行 linkgit:git-gc[1]:

    $ git gc

to recompress the archive.  This can be very time-consuming, so
you may prefer to run git-gc when you are not doing other work.

压缩操作比较耗时, 你运行linkgit:git-gc[1]命令最好是在你没有其它工作的时候.

### Ensuring reliability ###
### 保持可靠性 ###

The linkgit:git-fsck[1] command runs a number of self-consistency checks
on the repository, and reports on any problems.  This may take some
time.  The most common warning by far is about "dangling" objects:

linkgit:git-fsck[1] 运行一些仓库的一致性检查, 如果有任何问题就会报告. 这项操作也有点耗时, 通常报的警告就是“悬空对象"(dangling objects).

    $ git fsck
    dangling commit 7281251ddd2a61e38657c827739c57015671a6b3
    dangling commit 2706a059f258c6b245f298dc4ff2ccd30ec21a63
    dangling commit 13472b7c4b80851a1bc551779171dcb03655e9b5
    dangling blob 218761f9d90712d37a9c5e36f406f92202db07eb
    dangling commit bf093535a34a4d35731aa2bd90fe6b176302f14f
    dangling commit 8e4bec7f2ddaa268bef999853c25755452100f8e
    dangling tree d50bb86186bf27b681d25af89d3b5b68382e4085
    dangling tree b24c2473f1fd3d91352a624795be026d64c8841f
    ...

Dangling objects are not a problem.  At worst they may take up a little
extra disk space.  They can sometimes provide a last-resort method for
recovering lost work.

“悬空对象"(dangling objects)并不是问题, 最坏的情况只是它们多占了一些磁盘空间. 有时候它们是找回丢失的工作的最后一丝希望.