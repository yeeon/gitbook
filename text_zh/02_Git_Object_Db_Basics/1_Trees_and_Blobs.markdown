### Blob对象 ###

一个blob通常用来存储文件的内容.

[fig:object-blob]

You can use linkgit:git-show[1] to examine the contents of any blob. 
Assuming we have the SHA for a blob, we can examine its contents like this:

你可以使用linkgit:git-show[1]命令来查看一个blob对象里的内容。假设我们现在有一个Blob对象的SHA1哈希值，我们可以通过下面的的命令来查看内容：

    $ git show 6ff87c4664

     Note that the only valid version of the GPL as far as this project
     is concerned is _this_ particular version of the license (ie v2, not
     v2.2 or v3.x or whatever), unless explicitly otherwise stated.
    ...

A "blob" object is nothing but a chunk of binary data.  It doesn't refer
to anything else or have attributes of any kind, not even a file name.

一个blob对象就是一块二进制数据，它没有任何其它属性，甚至连文件名都没有。



Since the blob is entirely defined by its data, if two files in a
directory tree (or in multiple different versions of the repository)
have the same contents, they will share the same blob object. The object
is totally independent of its location in the directory tree, and
renaming a file does not change the object that file is associated with.

因为blob对象全部都是数据，如两个文件在一个目录树（或是一个版本仓库）中有同样的数据内容，那么它们将会共享同一个blob对象。Blob对象和其所对应的文件所在路径、文件名是否改被更改都没完没有关系。


### Tree 对象 ###

一个tree对象有一串(bunch)指向blob对象或是其它tree对象的指针，它一般用来来表示内容之间的目录层次关系。

[fig:object-tree]

The ever-versatile linkgit:git-show[1] command can also be used to
examine tree objects, but linkgit:git-ls-tree[1] will give you more
details.  Assuming we have the SHA for a tree, we can examine it like this:

linkgit:git-show[1]命令还可以用来查看tree对象，但是linkgit:git-ls-tree[1]能让你看到更多的细节。如果我们有一个tree对象的SHA1哈希值，我们可以像下面一样来查看它：


    $ git ls-tree fb3a8bdd0ce
    100644 blob 63c918c667fa005ff12ad89437f2fdc80926e21c    .gitignore
    100644 blob 5529b198e8d14decbe4ad99db3f7fb632de0439d    .mailmap
    100644 blob 6ff87c4664981e4397625791c8ea3bbb5f2279a3    COPYING
    040000 tree 2fb783e477100ce076f6bf57e4a6f026013dc745    Documentation
    100755 blob 3c0032cec592a765692234f1cba47dfdcc3a9200    GIT-VERSION-GEN
    100644 blob 289b046a443c0647624607d471289b2c7dcd470b    INSTALL
    100644 blob 4eb463797adc693dc168b926b6932ff53f17d0b1    Makefile
    100644 blob 548142c327a6790ff8821d67c2ee1eff7a656b52    README
    ...

As you can see, a tree object contains a list of entries, each with a
mode, object type, SHA1 name, and name, sorted by name.  It represents
the contents of a single directory tree.

就如同你所见，一个tree对象包括一串(list)条目，每一个条目包括：mode、对象类型、SHA1值 和名字(这串条目是按名字排序的)。它用来表示一个目录树的内容。

An object referenced by a tree may be blob, representing the contents of a
file, or another tree, representing the contents of a subdirectory.  Since
trees and blobs, like all other objects, are named by the SHA1 hash of their
contents, two trees have the same SHA1 name if and only if their contents
(including, recursively, the contents of all subdirectories) are identical.
This allows git to quickly determine the differences between two related tree
objects, since it can ignore any entries with identical object names.


一个tree对象可以指向(reference)：一个包含文件内容的blob对象，也可以是其它包含某个子目录内容的其它tree对象。Tree对象、blob对象和其它所有的对象一样，都用其内容的SHA1哈希值来命名的；只有当两个tree对象的内容完全相同（包括其所指向所有子对象）时，它的名字才会一样，反之亦然。这样就能让Git仅仅通过比较两个相关的tree对象的名字是否相同，来快速的判断其内容是否不同。


(Note: in the presence of submodules, trees may also have commits as
entries.  See the **Submodules** section.)

(注意：在submodules里，trees对象也可以指向commits对象. 请参见 **Submodules** 章节)

Note that the files all have mode 644 or 755: git actually only pays
attention to the executable bit.

注意：所有的文件的mode位都是644 或 755，这意味着Git只关心文件的可执行位.

 

