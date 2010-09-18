## The Git Object Model ##
## GIT对象模型 ##

### The SHA ###
### SHA ###

All the information needed to represent the history of a
project is stored in files referenced by a 40-digit "object name" that 
looks something like this:

所有用来表示项目历史信息的文件是通过一个40字符（40-digit）“对象名”，像这样的:

    6ff87c4664981e4397625791c8ea3bbb5f2279a3
    
You will see these 40-character strings all over the place in Git.
In each case the name is calculated by taking the SHA1 hash of the
contents of the object.  The SHA1 hash is a cryptographic hash function.
What that means to us is that it is virtually impossible to find two different
objects with the same name.  This has a number of advantages; among
others:

你会在Git里到处看到这种“40字符”字符串。每一个“对象名”都是通过对对象内容用SHA1做哈希计算得来的，（SHA1是一种密码学的哈希算法）。这样就意味着两个不同内容的对象不可能有相同的“对象名”。
    
这样做有会有几个好处：

- Git can quickly determine whether two objects are identical or not,
  just by comparing names.
- Since object names are computed the same way in every repository, the
  same content stored in two repositories will always be stored under
  the same name.
- Git can detect errors when it reads an object, by checking that the
  object's name is still the SHA1 hash of its contents.


1） Git比较对象名，可以很快的判断两个对象是否相同。

2） 因为在每个仓库（repository）的“对象名”的计算方法都完全一样，如果同样的内容存在两个不同的仓库中，就会存在相同的“对象名”下。

3） Git还可以通过检查对象内容的SHA1的哈希值和“对象名”是否相同，来判读对象内容是否正确。


### The Objects ###
### 对象 ###

Every object consists of three things - a **type**, a **size** and **content**.
The _size_ is simply the size of the contents, the contents depend on what
type of object it is, and there are four different types of objects: 
"blob", "tree", "commit", and "tag".

每个对象(object) 包括三个东东：**类型**，**大小**和**内容**。大小就是指内容的大小，内容取决于对象的类型，有四种类型的对象："blob"、"tree"、 "commit" 和"tag"。

- A **"blob"** is used to store file data - it is generally a file.
- A **"tree"** is basically like a directory - it references a bunch of
    other trees and/or blobs (i.e. files and sub-directories)
- A **"commit"** points to a single tree, marking it as what the project
    looked like at a certain point in time.  It contains meta-information
    about that point in time, such as a timestamp, the author of the changes
    since the last commit, a pointer to the previous commit(s), etc.
- A **"tag"** is a way to mark a specific commit as special in some way.  It
    is normally used to tag certain commits as specific releases or something
    along those lines.


1）**“blob”**用来存储文件数据，通常是一个文件

2）**“tree”**有点像一个目录，它管理一些**“tree”**或是 **“blob”**（就像文件和子目录）

3）一个**“commit”**指向一个"tree"，making it as what the project looked like at a certain point in time。它包括一些关于时间点的元数据，如时间戳、最近一次提交的作者、指前上次提交（commits）的指针等等。

4）一个**“tag”**是来标记某一个提交(commit) 的方法。

Almost all of Git is built around manipulating this simple structure of four
different object types.  It is sort of its own little filesystem that sits
on top of your machine's filesystem.

几乎所有的Git功能都是使用这四个简单的对象类型来完成的。它就是像是在你本机上构建一个小的文件系统。

### Different from SVN ###
### 与SVN的区别 ###

It is important to note that this is very different from most SCM systems
that you may be familiar with.  Subversion, CVS, Perforce, Mercurial and the
like all use _Delta Storage_ systems - they store the differences between one
commit and the next.  Git does not do this - it stores a snapshot of what all
the files in your project look like in this tree structure each time you
commit. This is a very important concept to understand when using Git.

Git与你熟悉的版本控制系统的差别是很大的。也许你熟悉Subversion、CVS、Perforce、Mercurial 等等，他们使用 _“增量文件系统”_ （Delta Storage systems）, 就是说它们存储每个次提交(commit)之间的差异。Git正好与之相反，它会把你的每次提交的文件的全部内容（snapshot）都会记录下来。这会是在使用Git时的一个很重要的理念。



 

 




 

 




 
