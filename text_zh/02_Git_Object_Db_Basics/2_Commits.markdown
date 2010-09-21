### Commit Object ###
### Commit对象 ###

The "commit" object links a physical state of a tree with a description
of how we got there and why. 

"commit对象"指向一个"tree对象", 并且带有相关的描述信息.

[fig:object-commit]

You can use the --pretty=raw option to
linkgit:git-show[1] or linkgit:git-log[1] to examine your favorite
commit:

你可以用 --pretty=raw 参数来配合 linkgit:git-show[1] 或 linkgit:git-log[1] 去查看某个提交(commit):


    $ git show -s --pretty=raw 2be7fcb476
    commit 2be7fcb4764f2dbcee52635b91fedb1b3dcf7ab4
    tree fb3a8bdd0ceddd019615af4d57a53f43d8cee2bf
    parent 257a84d9d02e90447b149af58b271c19405edb6a
    author Dave Watson <dwatson@mimvista.com> 1187576872 -0400
    committer Junio C Hamano <gitster@pobox.com> 1187591163 -0700

        Fix misspelling of 'suppress' in docs

        Signed-off-by: Junio C Hamano <gitster@pobox.com>

As you can see, a commit is defined by:

你可以看到, 一个提交(commit)由以下的部分组成:

- a **tree**: The SHA1 name of a tree object (as defined below), representing
  the contents of a directory at a certain point in time.

- 一个 **tree**: 

- **parent(s)**: The SHA1 name of some number of commits which represent the
  immediately previous step(s) in the history of the project.  The
  example above has one parent; merge commits may have more than
  one.  A commit with no parents is called a "root" commit, and
  represents the initial revision of a project.  Each project must have
  at least one root.  A project can also have multiple roots, though
  that isn't common (or necessarily a good idea).

- an **author**: The name of the person responsible for this change, together
  with its date.
- a **committer**: The name of the person who actually created the commit,
  with the date it was done.  This may be different from the author; for
  example, if the author wrote a patch and emailed it to another person who
  used the patch to create the commit.
- a **comment** describing this commit.

Note that a commit does not itself contain any information about what
actually changed; all changes are calculated by comparing the contents
of the tree referred to by this commit with the trees associated with
its parents.  In particular, git does not attempt to record file renames
explicitly, though it can identify cases where the existence of the same
file data at changing paths suggests a rename.  (See, for example, the
-M option to linkgit:git-diff[1]).

A commit is usually created by linkgit:git-commit[1], which creates a
commit whose parent is normally the current HEAD, and whose tree is
taken from the content currently stored in the index.

### 对象模型 ###

现在我们已经了解了3种主要对象类型(blob, tree 和 commit), 好现在就让我们大概了解一下它们怎么组合到一起的.

如果我们一个小项目, 有如下的目录结构:

    $>tree
    .
    |-- README
    `-- lib
        |-- inc
        |   `-- tricks.rb
        `-- mylib.rb

    2 directories, 3 files


如果我们把它提交(commit)到一个Git仓库中, 在Git中它们也许看起来就如下图:

[fig:objects-example]

你可以看到: 每个目录都创建了 **tree对象** (包括根目录), 每个文件都创建了一个对应的 **blob对象** . 最后有一个 **commit对象** 来指向根tree对象(root of trees), 这样我们就可以追踪项目每一项提交内容.