## Git Directory and Working Directory ##
## Git目录 与 工作目录 ##

### The Git Directory ###
### Git目录 ###

The 'git directory' is the directory that stores all Git's history and meta
information for your project - including all of the objects (commits, trees,
blobs, tags), all of the pointers to where different branches are and more.

'git目录'是为你的项目存储所有历史和元信息的目录 - 也包括所以的对象(commits,tress,blobs,tags), 这些对象也指向不同的分支.

There is only one Git Directory per project (as opposed to one per
subdirectory like with SVN or CVS), and that directory is (by default, though
not necessarily) '.git' in the root of your project.  If you look at the
contents of that directory, you can see all of your important files:

每一个项目只能有一个'Git目录'(这和SVN,CVS的每个子录都有相反),这个目录叫'.git'并且在你项目的根目录下(这是默认设置,但并不是必须的). 如果你查看这个目录的内容, 你可以看所有的重要文件:

    $>tree -L 1
    .
    |-- HEAD         # pointer to your current branch
    |-- config       # your configuration preferences
    |-- description  # description of your project 
    |-- hooks/       # pre/post action hooks
    |-- index        # index file (see next section)
    |-- logs/        # a history of where your branches have been
    |-- objects/     # your objects (commits, trees, blobs, tags)
    `-- refs/        # pointers to your branches

(there may be some other files/directories in there as well, but they are not important for now)
(也许现在还有其它 文件/目录 在 'Git目录' 里面, 但是现在它们并不重要)

### The Working Directory ###
### 工作目录 ###

The Git 'working directory' is the directory that holds the current checkout 
of the files you are working on.  Files in this directory are often removed
or replaced by Git as you switch branches - this is normal.  All your history 
is stored in the Git Directory; the working directory is simply a temporary 
checkout place where you can modify the files until your next commit.

Git的 '工作目录' 存储着你现在签出(checkout)来有于编辑的文件. 当你在项目的不同分支间切换时, 工作目录里的文件经常会被Git来替换和删除. 所有有历史信息都保存在 '中G目录   ;工作目录中只用来临时保存签出(checkout)) 文件的地方, 你可以编辑里面的文件直到下次提交(commit)为止.    