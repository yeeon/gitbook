## Git目录 与 工作目录 ##

### Git目录 ###

'Git目录'是为你的项目存储所有历史和元信息的目录 - 包括所以的对象(commits,tress,blobs,tags), 这些对象指向不同的分支.

每一个项目只能有一个'Git目录'(这和SVN,CVS的每个子目录中都有此类目录相反),　这个叫'.git'的目录在你项目的根目录下(这是默认设置,但并不是必须的). 如果你查看这个目录的内容, 你可以看所有的重要文件:

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

(也许现在还有其它 文件/目录 在 'Git目录' 里面, 但是现在它们并不重要)

### 工作目录 ###

Git的 '工作目录' 存储着你现在签出(checkout)来用来编辑的文件. 当你在项目的不同分支间切换时, 工作目录里的文件经常会被替换和删除. 所有有历史信息都保存在 'Git目录'中 ;　工作目录只用来临时保存签出(checkout) 文件的地方, 你可以编辑工作目录的文件直到下次提交(commit)为止.    