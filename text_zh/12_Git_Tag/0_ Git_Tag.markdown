## Git Tag ##
## Git标签 ##

### Lightweight Tags ###
### 轻量级标签 ###

We can create a tag to refer to a particular commit by running linkgit:git-tag[1]
with no arguments.

你可以用 linkgit:git-tag[1]不带任何参数创建一个标签(tag)指定某个提交(commit):

    $ git tag stable-1 1b2e1d63ff
    
After that, we can use stable-1 to refer to the commit 1b2e1d63ff.

这样，你就可以用stable-1 作为提交(commit) "1b2e1d63ff" 的代称。

This creates a "lightweight" tag, basically a branch that never moves.
If you would also like to include a comment with the tag,
and possibly sign it cryptographically, then we can create a *tag object* instead.

前面这样创建的是一个轻量级的标签",，这种分支通常是从来不移动的。
如果你想为一个标签(tag)添加注释，或是为它添加一个签名(sign it cryptographically),
那么我们就需要创建一个 *标签对象*.

### Tag Objects ###
### 标签对象 ###

If one of **-a**, **-s**, or **-u <key-id>** is passed, the command creates a tag object, 
and requires the tag message. Unless -m <msg> or -F <file> is given, an editor 
is started for the user to type in the tag message.


如果有 "-a", "-s" 或是 "-u <key-id>" 中间的一个命令参数被指定，那么就会创建
一个标签对象，并且需要一个标签消息(tag message). 如果没有"-m <msg>" 或是 
"-F <file>" 这些参数，那么一个编辑器就会启动来让用户输标签消息(tag message).

译者注：大家觉得这个标签消息是不是提交注释(commit comment)比较像。

When this happens, a new object is added to the Git object database and the 
tag ref points to that _tag object_, rather than the commit itself. The strength
of this is that you can sign the tag, so you can verify that it is the correct
commit later.  You can create a tag object like this:

当这样的一条命令执行后，一个新的对象被添加到Git对象库中，并且标签引用就指向了
一个标签对象，而不是指向一个提交(commit). 这样做的好处就是：你可以为一个标签
打处标记(sign), 方便你以后来查验这是不是一个正确的提交(commit).

下面是一个创建标签对象的例子:

    $ git tag -a stable-1 1b2e1d63ff
    
It is actually possible to tag any object, but tagging commit objects is the 
most common. (In the Linux kernel source, the first tag object
references a tree, rather than a commit)

标签对象可以指向任何对象，但是在通常情况下是一个提交(commit). (在Linux内核代
码中，第一个标签对象是指向一个树对象(tree),而不是指向一个提交(commit)).

### Signed Tags ###
### 签名的标签 ###

If you have a GPG key setup, you can create signed tags fairly easily.  First,
you will probably want to setup your key id in your _.git/config_ or _~.gitconfig_
file.

如果你配有GPG key,那么你就很容易创建签名的标签.首先你要在你的 _.git/config 或
_~.gitconfig里配好key.

下面是示例:

    [user]
        signingkey = <gpg-key-id>
        
You can also set that with

你也可以在命令行里直接指定:

    $ git config (--global) user.signingkey <gpg-key-id>
    
Now you can create a signed tag simply by replacing the **-a** with a **-s**.

现在你可以直接用"-s" 参数来创签名的标签。

    $ git tag -s stable-1 1b2e1d63ff
    
If you don't have your GPG key in your config file, you can accomplish the same
thing this way:

如果没有在配置文件中配GPG key,你可以用"-u“ 参数直接指定。
    
    $ git tag -u <gpg-key-id> stable-1 1b2e1d63ff