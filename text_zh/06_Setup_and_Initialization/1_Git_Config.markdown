### Git Config ###
### Git 配置 ###


使用Git的第一件事就是设置你的名字和email,这些就是你在提交commit时的签名。

    $ git config --global user.name "Scott Chacon"
    $ git config --global user.email "schacon@gmail.com"

That will set up a file in your home directory which may be used by any of
your projects. By default that file is *~/.gitconfig* and the contents will
look like this:

执行了上面的命令后,会在你的主目录(home directory)建立一个叫 *~/.gitconfig*  的文件.
内容一般像下面这样:
    [user]
            name = Scott Chacon
            email = schacon@gmail.com
            
If you want to override those values for a specific project (to use a work
email address, for example), you can run the *git config* command without the
*--global* option while in that project. This will add a [user] section like
the one shown above to the *.git/config* file in your project's root
directory.

如果你要针对不同的项目设置一个特定的值(例如把私人邮箱地址改为工作邮箱);你可以在项目中使用git config 命令不带 *--global* 选项来设置. 这会在你项目目录下的 *.git/config* 文件增加一节[user]内容(如上所示).

译者注: 这样就使某个项目的设置和全局设置有区别.