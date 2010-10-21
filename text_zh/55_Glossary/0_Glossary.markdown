## Glossary ##

Here we have the meanings of some terms used into Git context.  
These terms were entirely copied from 
[Git Glossary](http://www.kernel.org/pub/software/scm/git/docs/gitglossary.html).  

我们把在Git里常用的一些名词做了解释列在这里。
这些名词(terms)全部来自[Git Glossary](http://www.kernel.org/pub/software/scm/git/docs/gitglossary.html)。

_alternate object database_

>   Via the alternates mechanism, a repository
    can inherit part of its object database
    from another object database, which is called "alternate". 

_bare repository_

>   A bare repository is normally an appropriately
    named directory with a `.git` suffix that does not
    have a locally checked-out copy of any of the files under
    revision control. That is, all of the `git`
    administrative and control files that would normally be present in the
    hidden `.git` sub-directory are directly present in the
    `repository.git` directory instead,
    and no other files are present and checked out. Usually publishers of
    public repositories make bare repositories available.


_祼仓库_

>
    A bare repository is normally an appropriately
    named directory with a `.git` suffix that does not
    have a locally checked-out copy of any of the files under
    revision control. That is, all of the `git`
    administrative and control files that would normally be present in the
    hidden `.git` sub-directory are directly present in the
    `repository.git` directory instead,
    and no other files are present and checked out. Usually publishers of
    public repositories make bare repositories available.

    
_blob object_

>   Untyped object, e.g. the contents of a file.

_二进制对象_
>
    没有类型的数据对象。例如：一个文件的内容。
    
_branch_

>   A "branch" is an active line of development.  The most recent
    commit on a branch is referred to as the tip of
    that branch.  The tip of the branch is referenced by a branch
    head, which moves forward as additional development
    is done on the branch.  A single git
    repository can track an arbitrary number of
    branches, but your working tree is
    associated with just one of them (the "current" or "checked out"
    branch), and HEAD points to that branch.

_分支_
>
    一个“分支”是开发过程中的(active line)。。。。

_cache_

>   Obsolete for: index.

_缓存_

>   索引(index)的旧称(obsolete).

_chain_

>   A list of objects, where each object in the list contains
    a reference to its successor (for example, the successor of a
    commit could be one of its parents).

_链表_

>   一串对象，其中每个对象都有指向其后继对象指针(reference to its successor)。例如：一个提交(commit)的后继对象就是它的父对象。

_changeset_

>   BitKeeper/cvsps speak for "commit". Since git does not
    store changes, but states, it really does not make sense to use the term
    "changesets" with git.

_修改集_

>   BitKeeper/cvsps 里对于提交(commit)的说法。但是 git 只存储状态(states)，不存储修改；所以这个词用在 git 里真是不大合适。

_checkout_

>   The action of updating all or part of the
    working tree with a tree object
    or blob from the
    object database, and updating the
    index and HEAD if the whole working tree has
    been pointed at a new branch.

_checkout (签出)_
>
    用对象仓库(object database)里的一个树对象(tree object)更新当前整个工作树(worktree)，或者一个二进制对象(blob object)更新工作树的一部分；如果工作树指向了一个新的分支，那么就会更新索引(index)和HEAD。

_cherry-picking_

>   In SCM jargon, "cherry pick" means to choose a subset of
    changes out of a series of changes (typically commits) and record them
    as a new series of changes on top of a different codebase. In GIT, this is
    performed by the "git cherry-pick" command to extract the change introduced
    by an existing commit and to record it based on the tip
    of the current branch as a new commit.

_cherry-picking_

>   在SCM的行话里，“cherry pick“ 意味着从一系列的修改中选出一部分修改(通常是提交)，应用到当前代码中。()

_clean_

>   A working tree is clean, if it
    corresponds to the revision referenced by the current
    head. Also see "dirty".

_干净_

>   如一个工作树(working tree)中所有的修改都已提交到了当前分支里(current head)，那么就说它是干净的(clean)，

_commit_

>   As a noun: A single point in the
    git history; the entire history of a project is represented as a
    set of interrelated commits.  The word "commit" is often
    used by git in the same places other revision control systems
    use the words "revision" or "version".  Also used as a short
    hand for commit object.

>   As a verb: The action of storing a new snapshot of the project's
    state in the git history, by creating a new commit representing the current
    state of the index and advancing HEAD
    to point at the new commit.


_提交_

>
    作为名词：指向git历史的某一点的指针；整个项目的历史就由一组相互关联的提交组成的。提交(commit)在其它版本控制系统中也做"revision"或"version"。同时做为提交对象(commit object)的缩写。

>
    作为动词：创建一新的提交(commit)来表示当前索引(index)的状态，把 HEAD 指向新创建的提交，这一系列把项目在某一时间上的快照(snapshot)保存在git历史中的操作。

_commit object_

>   An object which contains the information about a
    particular revision, such as parents, committer,
    author, date and the tree object which corresponds
    to the top directory of the stored
    revision.

_提交对象_

>   一个关于特定版本信息(particular revision)的对象。包括父对象名，提交者，作者，日期和存储了此版本内容的树对象名。
        

_core git_

>   Fundamental data structures and utilities of git. Exposes only limited
    source code management tools.

_core git_

>   Git的基本数据结构和工具。它只对外提供简单的代码管理工具。

_DAG_

>   Directed acyclic graph. The commit objects form a
    directed acyclic graph, because they have parents (directed), and the
    graph of commit objects is acyclic (there is no chain
    which begins and ends with the same object).

_DAG_

>   有向无环图。众多提交对象(commit objects)组成了一个有向无环图；因为它们有直接父对象(direct parent)，且没有一条提交线路(chain)的起点和终点都是同一个对象。

_dangling object_

>   An unreachable object which is not
    reachable even from other unreachable objects; a
    dangling object has no references to it from any
    reference or object in the repository.

_悬空对象_

>   
    一个甚至从其它不可达对象也不可达的对象(unreachable object)；仓库里的一个悬空对象没有任何引用(reference)或是对象(object)引用它。

_detached HEAD_

>   Normally the HEAD stores the name of a
>   branch.  However, git also allows you to check out
>   an arbitrary commit that isn't necessarily the tip of any
>   particular branch.  In this case HEAD is said to be "detached".


_分离的HEAD_

>   通常情况下HEAD里是存放当前分支的名字。然而 git 有时也允许你签出任意的一个提交(commit)，而不一定是某分支的最近的提交；在这种情况下，HEAD就是处于分离的状态(detached)。 
>   译者注：这时`.git/HEAD`中存储的就是签出的提交的SHA串值。


_dircache_

>   You are *waaaaay* behind. See index.

_dircache_

>   请参见索引(index)。

_directory_

>   The list you get with "ls" :-)

_目录_

>   执行"ls"命令所显示的结果 :-)

_dirty_

>   A working tree is said to be "dirty" if
    it contains modifications which have not been committed to the current
    branch.

_脏_

>  一个工作树里有没有提交到当前分支里修改，那么我就说它是脏的"dirty"。


_ent_

>   Favorite synonym to "tree-ish" by some total geeks. See
    `http://en.wikipedia.org/wiki/Ent_(Middle-earth)` for an in-depth
    explanation. Avoid this term, not to confuse people.


_ent_

>   某些人给树名(tree-ish)起的另外一个别名，这里`http://en.wikipedia.org/wiki/Ent_(Middle-earth)`有更详细的解释。最好不要使用这个名词，以免让大家糊涂。

_evil merge_

>   An evil merge is a merge that introduces changes that
    do not appear in any parent.


_坏的合并_

>   如果一次合并引入一些不存在于任何父对象(parent)中的修改，那么就称它是一个坏的合并(evil merge)。

_fast forward_

>   A fast-forward is a special type of merge where you have a
    revision and you are "merging" another
    branch's changes that happen to be a descendant of what
    you have. In such these cases, you do not make a new merge
    commit but instead just update to his
    revision. This will happen frequently on a
    tracking branch of a remote
    repository.

_快速向前_

>   “fast-forward”是一种特殊的合并,()。
>   在这种情况下，并没有创建一个合并提交(merge commit)，只是更新了版本信息。
>   当本地分支是远端仓库(remote repository)的跟踪分支时，这种情况经常出现。

_fetch_

>   Fetching a branch means to get the
    branch's head ref from a remote
    repository, to find out which objects are
    missing from the local object database,
    and to get them, too.  See also linkgit:git-fetch[1].

_抓取_

>   抓取一个分支意味着：得到远端仓库(remote repository)分支的head ref，找出本地对象数据库所缺少的对象，并把它们下载下来。你可以参考一下 linkgit:git-fetch[1]。

_file system_

>   Linus Torvalds originally designed git to be a user space file system,
    i.e. the infrastructure to hold files and directories. That ensured the
    efficiency and speed of git.

_文件系统_

>   Linus Torvalds 最初设计git时，是把它设计在一个用户空间(user space)文件系统；也就是一个来保存文件和目录的 infrastructure。这样就保证了git的速度和效率。

_git archive_

>   Synonym for repository (for arch people).

_git archive_

>   对玩架构的人来说，这就是仓库的同义词。

_grafts_

>   Grafts enables two otherwise different lines of development to be joined
    together by recording fake ancestry information for commits. This way
    you can make git pretend the set of parents a commit has
    is different from what was recorded when the commit was
    created. Configured via the `.git/info/grafts` file.

_hash_

>   In git's context, synonym to object name.

_哈希_

>   在git里，这就是对象名(object name)的同义词。

_head_

>   A named reference to the commit at the tip of a
    branch.  Heads are stored in
    `$GIT_DIR/refs/heads/`, except when using packed refs. (See
    linkgit:git-pack-refs[1].)

_head_

>   指向一个分支最新提交的命名引用(named reference)。Heads 一般存储在 `$GIT_DIR/refs/heads/`，除非使用了打包引用(packed refs)。
    参见: linkgit:git-pack-refs[1]

_HEAD_

>   The current branch.  In more detail: Your working tree is normally derived 
    from the state of the tree referred to by HEAD.  HEAD is a reference to one
    of the heads in your repository, except when using a detached HEAD, in which
    case it may	reference an arbitrary commit.

_HEAD_

>   当前分支。更准确的说，你的工作树(working tree)通是从HEAD所指向的tree所派生的来的。
>   HEAD 必须是指向一个你仓库里的head，除非你使用分离的HEAD(detached HEAD)。

_head ref_

>   A synonym for head.

_head ref_

>   head的同义词。

_hook_

>   During the normal execution of several git commands, call-outs are made
    to optional scripts that allow a developer to add functionality or
    checking. Typically, the hooks allow for a command to be pre-verified
    and potentially aborted, and allow for a post-notification after the
    operation is done. The hook scripts are found in the
    `$GIT_DIR/hooks/` directory, and are enabled by simply
    removing the `.sample` suffix from the filename. In earlier versions
    of git you had to make them executable.

_钩子_

>   在一些git命令的执行过程中, () 允许开发人员调用特别的脚本来添加功能或检查。
    ()
    
    Typically，钩子允许对一个命令做pre-verified并且可以中止此命令的运行；同时也可在这个命令执行完后做后继的通知工作。这些钩子脚本放在`$GIT_DIR/hooks/`目录下，你只要把这它们文件名的`.sample`后缀删掉就可以了。不过在git的早期版本，你需要为这些钩子脚本加上可执行属性。

_index_

>   A collection of files with stat information, whose contents are stored
    as objects. The index is a stored version of your
    working tree. Truth be told, it can also contain a second, and even
    a third version of a working tree, which are used
    when merging.

_索引_

>   描述项目状态信息的文件，。索引里保存的是你的工作树的版本记录。()

_index entry_

>   The information regarding a particular file, stored in the
    index. An index entry can be unmerged, if a
    merge was started, but not yet finished (i.e. if
    the index contains multiple versions of that file).


_索引条目_

>   

_master_

>   The default development branch. Whenever you
    create a git repository, a branch named
    "master" is created, and becomes the active branch. In most
    cases, this contains the local development, though that is
    purely by convention and is not required.

_主分支 (master)_

>   默认的开发分支。当你创建了一个git仓库，一个叫"master"的分支就被创建并且成为当前分支(active branch)。在多数情况下，这个分支里就包含有本地的开发内容。

_merge_

>   As a verb: To bring the contents of another
    branch (possibly from an external
    repository) into the current branch.  In the
    case where the merged-in branch is from a different repository,
    this is done by first fetching the remote branch
    and then merging the result into the current branch.  This
    combination of fetch and merge operations is called a
    pull.  Merging is performed by an automatic process
    that identifies changes made since the branches diverged, and
    then applies all those changes together.  In cases where changes
    conflict, manual intervention may be required to complete the
    merge.

>   As a noun: unless it is a fast forward, a
    successful merge results in the creation of a new commit
    representing the result of the merge, and having as
    parents the tips of the merged branches.
    This commit is referred to as a "merge commit", or sometimes just a
    "merge".

_merge_

>   作为动词：把另外一个分支(也许来自另外一个仓库)的内容合并进当前的分支。

>   作为名词：除非合并的结果是 fast forward；一次成功的合并会创建一个提交(commit) --()。这个提交(commit)也可以表述为“合并提交”(merge commit)，或者就是"合并"(merge 名词)。

_object_

>   The unit of storage in git. It is uniquely identified by the
    SHA1> of its contents. Consequently, an
    object can not be changed.

_对象_

>   Git的存储单位，它以对象内容的SHA1值做为不重复的对象名；因此对象内容是不能被修改的。

_object database_

>   Stores a set of "objects", and an individual object is
    identified by its object name. The objects usually
    live in `$GIT_DIR/objects/`.

_object identifier_

>   Synonym for object name.

_对象标识符_

>   对象名(object name)的同义词。

_object name_

>   The unique identifier of an object. The hash
    of the object's contents using the Secure Hash Algorithm
    1 and usually represented by the 40 character hexadecimal encoding of
    the hash of the object.

_对象名_

>   一个对象的唯一标识符(unique identifier)。它是使用SHA1算法(Secure Hash Algorithm 1)给对象内容进行哈希(hash)计算，产生的一个40个字节长的16进制编码的串。

_object type_

>   One of the identifiers "commit", "tree", "tag" or "blob" describing the 
    type of an object.

_对象类型_

>   有4种对象类型：提交(commit)，树(tree)，标签(tag)和二进制块(blob)。

_octopus_

>   To merge more than two branches. Also denotes an
    intelligent predator.

_章鱼_

>   多于两个分支的合并(merge)。也用来表示聪明的肉食动物。


_origin_

>   The default upstream repository. Most projects have
    at least one upstream project which they track. By default
    'origin' is used for that purpose. New upstream updates
    will be fetched into remote tracking branches named
    origin/name-of-upstream-branch, which you can see using
    "`git branch -r`".

_原始_

>   默认的上游仓库(upstream repository)。每个项目至少有一个它追踪(track)的上游(upstream)，通常情况 origin 就是用于这种目的。你可以用 ”｀git branch -r`" 命令查看上游仓库(upstream repository)里所有的分支，再用 origin/name-of-upstream-branch 的名字来抓取(fetch)远程追踪分支里的内容。

_pack_

>   A set of objects which have been compressed into one file (to save space
    or to transmit them efficiently).

_包_

>   一个文件，里面有一些压缩了的对象。(用以节约空间或是提高传输效率)。

_pack index_

>   The list of identifiers, and other information, of the objects in a
    pack, to assist in efficiently accessing the contents of a
    pack.

_包索引_

>   包(pack)里的一些标识符和其它相关信息，用于帮助git快速的访问包(pack)里面的对象。

_parent_

>   A commit object contains a (possibly empty) list
    of the logical predecessor(s) in the line of development, i.e. its
    parents.

_父对象_

>   一个提交对象(commit object)，()。

_pickaxe_

>   The term pickaxe refers to an option to the diffcore
    routines that help select changes that add or delete a given text
    string. With the `--pickaxe-all` option, it can be used to view the full
    changeset that introduced or removed, say, a
    particular line of text. See linkgit:git-diff[1].

_plumbing_

>   Cute name for core git.

_plumbing_

>   core git的别名(cute name)。

_porcelain_

>   Cute name for programs and program suites depending on
    core git, presenting a high level access to
    core git. Porcelains expose more of a SCM
    interface than the plumbing.

_pull_

>   Pulling a branch means to fetch it and
    merge it.  See also linkgit:git-pull[1].

_拉_

>   拉(pull)一个分支意味着，把它抓取(fetch)下来并合并(merge)进当前的分支。可以参考 linkgit:git-pull[1].

_push_

>   Pushing a branch means to get the branch's
    head ref from a remote repository,
    find out if it is a direct ancestor to the branch's local
    head ref, and in that case, putting all
    objects, which are reachable from the local
    head ref, and which are missing from the remote
    repository, into the remote
    object database, and updating the remote
    head ref. If the remote head is not an
    ancestor to the local head, the push fails.

_推_

>   ()

_reachable_

>   All of the ancestors of a given commit are said to be
    "reachable" from that commit. More
    generally, one object is reachable from
    another if we can reach the one from the other by a chain
    that follows tags to whatever they tag,
    commits to their parents or trees, and
    trees to the trees or blobs
    that they contain.


_可达的_

>   

_rebase_

>   To reapply a series of changes from a branch to a
    different base, and reset the head of that branch
    to the result.

_rebase_

>   重新应用(reapply)当前分支(branch)和另一个分支(base)间的修改；并且根据rebase的结果重置当前分支的 head。

_ref_

>   A 40-byte hex representation of a SHA1 or a name that
    denotes a particular object. These may be stored in
    `$GIT_DIR/refs/`.

_引用_

>   一个40字节长的SHA1串或是指向某个对象的名字。它们可能存储在 `$GIT_DIR/refs/`。

_reflog_

>   A reflog shows the local "history" of a ref.  In other words,
    it can tell you what the 3rd last revision in _this_ repository
    was, and what was the current state in _this_ repository,
    yesterday 9:14pm.  See linkgit:git-reflog[1] for details.

_reflog_

>   reflog用以表示本地的ref的历史记录。从另外一角度也可以说，它能行告诉你这个仓库最近的第3个版本(revision)是什么，昨天晚上9点14分时你是在这个仓库的哪个分支下工作。可以参见:linkgit:git-reflog[1]。

_refspec_

>   A "refspec" is used by fetch and
    push to describe the mapping between remote
    ref and local ref. They are combined with a colon in
    the format <src>:<dst>, preceded by an optional plus sign, +.
    For example: `git fetch $URL
    refs/heads/master:refs/heads/origin` means "grab the master
    branch head from the $URL and store
    it as my origin branch head". And `git push
    $URL refs/heads/master:refs/heads/to-upstream` means "publish my
    master branch head as to-upstream branch at $URL". See also
    

_refspec_

>   "refspec"在抓取和推的过程中描述远程ref和本地ref之间的映射关系。它用冒号连接：<src>:<dst>，前面也可以加一个加号：“+“。
    例如：`git fetch $URL refs/heads/master:refs/heads/origin` 意味着：从$URL抓取主分支的 head 并把它保存到本地的origin分支的head中。`git push $URL refs/heads/master:refs/heads/to-upstream` 意味着：把我的主分支 head 推到$URL上的 to-upstream分支里。可以参见： linkgit:git-push[1]。

_repository_

>   A collection of refs together with an
    object database containing all objects
    which are reachable from the refs, possibly
    accompanied by meta data from one or more porcelains. A
    repository can share an object database with other repositories
    via alternates mechanism.

_resolve_

>   The action of fixing up manually what a failed automatic
    merge left behind.

_resolve_

>   在自动合并失败后，手工修复合冲突的行为。

_revision_

>   A particular state of files and directories which was stored in the
    object database. It is referenced by a
    commit object.

_版本_

>   保存对象仓库(object database)的文件和目录某一特定时间点的状态；它会被一个提交对象(commit object)所引用。

_rewind_

>   To throw away part of the development, i.e. to assign the
    head to an earlier revision.

_rewind_

>   To throw away part of the development, i.e. to assign the
    head to an earlier revision.

_rewind_

>   丢弃某一部分开发成果。例如：把head 指向早期的版本。

_SCM_

>   Source code management (tool).

_SCM_

>   源代码管理工作。

_SHA1_

>   Synonym for object name.

_SHA1_

>   对象名(object name)的同义词。

_shallow repository_

>   A shallow repository has an incomplete
    history some of whose commits have parents cauterized away (in other
    words, git is told to pretend that these commits do not have the
    parents, even though they are recorded in the commit
    object). This is sometimes useful when you are interested only in the
    recent history of a project even though the real history recorded in the
    upstream is much larger. A shallow repository
    is created by giving the `--depth` option to linkgit:git-clone[1], and
    its history can be later deepened with linkgit:git-fetch[1].

_symref_

>   Symbolic reference: instead of containing the SHA1
    id itself, it is of the format 'ref: refs/some/thing' and when
    referenced, it recursively dereferences to this reference.
    'HEAD' is a prime example of a symref. Symbolic
    references are manipulated with the linkgit:git-symbolic-ref[1]
    command.

_tag_

>   A ref pointing to a tag or
    commit object. In contrast to a head,
    a tag is not changed by a commit. Tags (not
    tag objects) are stored in `$GIT_DIR/refs/tags/`. A
    git tag has nothing to do with a Lisp tag (which would be
    called an object type in git's context). A
    tag is most typically used to mark a particular point in the
    commit ancestry chain.


_标签_

>   一个ref指向一个标签或提交对象。与 head 相反，标签并不会在一次提交操作后改变。标签(不是标签对象)存储在`$GIT_DIR/refs/tags/`。 一个标签通常是用来标识提交家族链(commit ancerstry chain)里的某一点。


_tag object_

>   An object containing a ref pointing to
    another object, which can contain a message just like a
    commit object. It can also contain a (PGP)
    signature, in which case it is called a "signed tag object".

_标签对象_

>   一个含有指向其它对象的引用(ref)的对象，对象里也包括有注释消息。如果它里面可以含有一个PGP签名，那么就称为一个“签名标签对象”。

_topic branch_

>   A regular git branch that is used by a developer to
    identify a conceptual line of development. Since branches are very easy
    and inexpensive, it is often desirable to have several small branches
    that each contain very well defined concepts or small incremental yet
    related changes.

_tracking branch_

>   A regular git branch that is used to follow changes from
    another repository. A tracking
    branch should not contain direct modifications or have local commits
    made to it. A tracking branch can usually be
    identified as the right-hand-side ref in a Pull:

    refspec.

_追踪分支_

>   一个用以追踪(follow)另外一个仓库的修改的git分支。()

_tree_

>   Either a working tree, or a tree object together with the dependent 
    blob and tree objects (i.e. a stored representation of a working tree).

_树_

>  
   可以是一个工作树(working tree)，也可以是一个树对象(tree object)。

_tree object_

>   An object containing a list of file names and modes along
    with refs to the associated blob and/or tree objects. A
    tree is equivalent to a directory.


_树对象_

>   包含有一串(list)文件名和模式(mode)，并且指向与之相关的二进制对象(blob object)和树对象(tree object)。一个树(tree)等价于一个目录。

_tree-ish_

>   A ref pointing to either a commit object, a tree object, or a tag
    object pointing to a tag or commit or tree object.

_树名_

>   
    一个指向的提交对象(commit object)，树对象(tree object)或是标签对象(tag object)的引用(ref)。

_unmerged index_

>   An index which contains unmerged
    index entries.

_未合并索引_

>   一个索引中包含有未合并的索引条目(index entries)。

_unreachable object_

>   An object which is not reachable from a
    branch, tag, or any other reference.

_不可达对象_

>   从任何一个分支、标签或是其它引用(reference)做为起点都无法到达的一个对象。

_working tree_

>   The tree of actual checked out files.  The working tree is
    normally equal to the HEAD plus any local changes
    that you have made but not yet committed.

_工作树_

>   
    签出(checkout)用于编辑的文件目录树。 工作树一般等价于HEAD加本地没有提交的修改。
 