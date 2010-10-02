## 传输协议 ##

Here we will go over how clients and servers talk to each other to 
transfer Git data around.

这里我们要看一下: Git的客户端和服务器如何交互传输数据.


### Fetching Data over HTTP ###
### 通过HTTP协议传输 ###

Fetching over an http/s URL will make Git use a slightly dumber protocol.


In this case, all of the logic is entirely on the client side.  The server
requires no special setup - any static webserver will work fine if the
git directory you are fetching from is in the webserver path.

使用http协议, 所有的逻辑计算(logic)都是在客户端进行. 服务器不需要特别的设置, 你只要把git目录放到一个可以访问的web目录即可.

In order for this to work, you do need to run a single command on the 
server repo everytime anything is updated, though - linkgit:git-update-server-info[0],
which updates the objects/info/packs and info/refs files to list which refs
and packfiles are available, since you can't do a listing over http.  When
that command is run, the objects/info/packs file looks something like this:

为了通过http访问, 当你的仓库有任何更新时, 需要运行一个命令: linkgit:git-update-server-info[0]. 因为web服务器一般不允许执行列出目录中文件的操作, 所以linkgit:git-update-server-info[0]命令把“objects/info/packs"目录和"info/refs"目录下的文件放到一个列表中. 当这个命令执行后,"objects/info/packs"文件看起来就会像下面一样:

	P pack-ce2bd34abc3d8ebc5922dc81b2e1f30bf17c10cc.pack
	P pack-7ad5f5d05f5e20025898c95296fe4b9c861246d8.pack

So that if the fetch can't find a loose file, it can try these packfiles.  The
info/refs file will look something like this:

如果通过http协议拉取数据的过程中找不到松散文件(loose file), git就会去尝试查找打包文件(packfiles). "info/refs" 文件的内容看起来就下面这样:

	184063c9b594f8968d61a686b2f6052779551613	refs/heads/development
	32aae7aef7a412d62192f710f2130302997ec883	refs/heads/master

Then when you fetch from this repo, it will start with these refs and walk the
commit objects until the client has all the objects that it needs. 

当你从这个仓库开始抓取(fetch)数据时, git就会从这些引用(refs)开始遍历查找所有的提交对象(commit objects), 直到客户端得到了它所有需要的所有对象为止.

For instance, if you ask to fetch the master branch, it will see that master is
pointing to <code>32aae7ae</code> and that your master is pointing to <code>ab04d88</code>,
so you need <code>32aae7ae</code>.  You fetch that object 

例如, 你要抓取到(fetch)服务器上的"master"分支; git看到服务器上的"master"分支指向`32aae7ae`, 而你当前的"master"分支是指向`ab04d88`. 那么很明显, 你需要得到`32aae7ae`这个对象. 

下面就是抓取时的交互过程(http协议层):


	CONNECT http://myserver.com
	GET /git/myproject.git/objects/32/aae7aef7a412d62192f710f2130302997ec883 - 200
	
and it looks like this:

然后返回信息看起来就像下面这样:

	tree aa176fb83a47d00386be237b450fb9dfb5be251a
	parent bd71cad2d597d0f1827d4a3f67bb96a646f02889
	author Scott Chacon <schacon@gmail.com> 1220463037 -0700
	committer Scott Chacon <schacon@gmail.com> 1220463037 -0700

	added chapters on private repo setup, scm migration, raw git

So now it fetches the tree <code>aa176fb8</code>:

好的那么现在它就是开始抓取树对象(tree) `aa176fb8`:
译者注:`32aae7ae`提交对象(commit object)指向树对象(tree) `aa176fb8`

	GET /git/myproject.git/objects/aa/176fb83a47d00386be237b450fb9dfb5be251a - 200

which looks like this:

下面这些是返回的树对象(tree)信息:

	100644 blob 6ff87c4664981e4397625791c8ea3bbb5f2279a3	COPYING
	100644 blob 97b51a6d3685b093cfb345c9e79516e5099a13fb	README
	100644 blob 9d1b23b8660817e4a74006f15fae86e2a508c573	Rakefile

So then it fetches those objects:

很明显, 树对象(tree)里有3个文件(blob). 好的, 我们就把它们抓下来吧:

	GET /git/myproject.git/objects/6f/f87c4664981e4397625791c8ea3bbb5f2279a3 - 200
	GET /git/myproject.git/objects/97/b51a6d3685b093cfb345c9e79516e5099a13fb - 200
	GET /git/myproject.git/objects/9d/1b23b8660817e4a74006f15fae86e2a508c573 - 200

It actually does this with Curl, and can open up multiple parallel threads to 
speed up this process.  When it's done recursing the tree pointed to by the 
commit, it fetches the next parent.
	
这项http下载操作实际上是由curl来做的, 我们可以开多个并行的线程来加快下载速度. Git遍历完提交对象(commit)所指向的树对象(tree)后, 就会开始抓取提交对象(commit)的父对象(next parent). 

	GET /git/myproject.git/objects/bd/71cad2d597d0f1827d4a3f67bb96a646f02889 - 200

Now in this case, the commit that comes back looks like this:

返回的父对象(parent commit object)信息就如下面所示:

	tree b4cc00cf8546edd4fcf29defc3aec14de53e6cf8
	parent ab04d884140f7b0cf8bbf86d6883869f16a46f65
	author Scott Chacon <schacon@gmail.com> 1220421161 -0700
	committer Scott Chacon <schacon@gmail.com> 1220421161 -0700

	added chapters on the packfile and how git stores objects
	
and we can see that the parent, <code>ab04d88</code> is where our master branch
is currently pointing.  So, we recursively fetch this tree and then stop, since
we know we have everything before this point.  You can force Git to double check
that we have everything with the '--recover' option.  See linkgit:git-http-fetch[1]
for more information.

我们现在可以看到`ab04d88`是返回的提交对象(commit)的父对象, 而`ab04d88`(commit)就是我们当前的"master"分支. 那么我们只需要得到树对象(tree):`b4cc00c`就可以了, 因为之前的所以的提交(commit)我们都有了. 为了保险起见, 你也可以加上'--recover'参数, 强制git反复检查我们是否拥有所有的对象. 你可以点这里: linkgit:git-http-fetch[1] 查看更多信息:

If one of the loose object fetches fails, Git will download the packfile indexes
looking for the sha that it needs, then download that packfile. 

如果有一个松散对象(loose object)下载失败了, git会下载打包文件索引(packfile indexes), 通过它来查找对应的sha串值，然后再下载对应的打包文件(packfile).

It is important if you are running a git server that serves repos this way to
implement a post-receive hook that runs the 'git update-server-info' command
each time or there will be confusion.	

你一定要在git服务器的仓库里添一个"post-receive"钩子(hook), 这个钩子(hook)会执行'git update-server-info; 否则仓库的信息就得不到更新.


### Fetching Data with Upload Pack ###
### 通过 Upload Pack 传输数据 ###


For the smarter protocols, fetching objects is much more efficient.  A socket
is opened, either over ssh or over port 9418 (in the case of the git:// protocol),
and the linkgit:git-fetch-pack[1] command on the client begins communicating with
a forked linkgit:git-upload-pack[1] process on the server.

对于一个聪明的协议, 抓取对象的过程(fetching objects)应当更加高效. 不管是用通过ssh协议还是git协议(git:// 协议，在9418端口上运行), 当客户端和服务器建立了一个socket连接后，客户端开始运行:linkgit:git-fetch-pack命令, 和服务器创建(fork)的 linkgit:git-update-pack[1]进行通讯.


Then the server will tell the client which SHAs it has for each ref,
and the client figures out what it needs and responds with a list of SHAs it
wants and already has.


At this point, the server will generate a packfile with all the objects that 
the client needs and begin streaming it down to the client.

这里, 服务器会把客户端需要的所有对象打一个包(packfile), 然后再传送给客户端.

Let's look at an example.

让我们来看一个例子.

The client connects and sends the request header. The clone command

客户端连接并且发送请求头(request header). 例如，克隆命令:

	$ git clone git://myserver.com/project.git

produces the following request:

上面的命令会产生下面的请求:

	0032git-upload-pack /project.git\\000host=myserver.com\\000

The first four bytes contain the hex length of the line (including 4 byte line
length and trailing newline if present). Following are the command and
arguments. This is followed by a null byte and then the host information. The
request is terminated by a null byte.

最前面的4个字节表示一行的16进行制长试(hex length) (包括这个4个字节,但不包括换行符). 下面接着的是命令和参数, 这之后是一个null字节(\\000)和主机信息. 请求的结尾是以null字节结束的.


The request is processed and turned into a call to git-upload-pack:

这个请求被服务器接收并且转换成对"git-upload-pack"的命令调用.

 	$ git-upload-pack /path/to/repos/project.git

This immediately returns information of the repo:

这条命令会马上返回仓库的信息:


	007c74730d410fcb6603ace96f1dc55ea6196122532d HEAD\\000multi_ack thin-pack side-band side-band-64k ofs-delta shallow no-progress
	003e7d1665144a3a975c05f1f43902ddaf084e784dbe refs/heads/debug
	003d5a3f6be755bbb7deae50065988cbfa1ffa9ab68a refs/heads/dist
	003e7e47fe2bd8d01d481f44d7af0531bd93d3b21c01 refs/heads/local
	003f74730d410fcb6603ace96f1dc55ea6196122532d refs/heads/master
	0000

Each line starts with a four byte line length declaration in hex. The section
is terminated by a line length declaration of 0000.

每一行开始的头4个字节表示此行的长度(以16进制表示). 这块(section)信息以一行“0000”为结束标识符.

This is sent back to the client verbatim. The client responds with another
request:

上面这些服务器产生的数据被发送回客户端. 然后客户端用另外一个请求做为响应:

	0054want 74730d410fcb6603ace96f1dc55ea6196122532d multi_ack side-band-64k ofs-delta
p	0032want 7d1665144a3a975c05f1f43902ddaf084e784dbe
	0032want 5a3f6be755bbb7deae50065988cbfa1ffa9ab68a
	0032want 7e47fe2bd8d01d481f44d7af0531bd93d3b21c01
	0032want 74730d410fcb6603ace96f1dc55ea6196122532d
	00000009done

The is sent to the open git-upload-pack process which then streams out the 
final response:

上面这些客户客户端的请求会被发送到新建的"git-upload-pack"进程, 这个进程会返回(streams out)最终的结果(final response):

	"0008NAK\n"
	"0023\\002Counting objects: 2797, done.\n"
	"002b\\002Compressing objects:   0% (1/1177)   \r"
	"002c\\002Compressing objects:   1% (12/1177)   \r"
	"002c\\002Compressing objects:   2% (24/1177)   \r"
	"002c\\002Compressing objects:   3% (36/1177)   \r"
	"002c\\002Compressing objects:   4% (48/1177)   \r"
	"002c\\002Compressing objects:   5% (59/1177)   \r"
	"002c\\002Compressing objects:   6% (71/1177)   \r"
	"0053\\002Compressing objects:   7% (83/1177)   \rCompressing objects:   8% (95/1177)   \r"
	...
	"005b\\002Compressing objects: 100% (1177/1177)   \rCompressing objects: 100% (1177/1177), done.\n"
	"2004\\001PACK\\000\\000\\000\\002\\000\\000\n\\355\\225\\017x\\234\\235\\216K\n\\302"...
	"2005\\001\\360\\204{\\225\\376\\330\\345]z\226\273"...
	...
	"0037\\002Total 2797 (delta 1799), reused 2360 (delta 1529)\n"
	...
	"<\\276\\255L\\273s\\005\\001w0006\\001[0000"
	
See the Packfile chapter previously for the actual format of the packfile data
in the response.

你可以查看打包文件(packfile)这一章, 了解响应内容中的打包文件(packfile)的实际格式.
	
### Pushing Data ###
##＃ 推数据 ###

Pushing data over the git and ssh protocols is similar, but simpler.  Basically
what happens is the client requests a receive-pack instance, which is started
up if the client has access, then the server returns all the ref head shas it
has again and the client generates a packfile of everything the server needs
(generally only if what is on the server is a direct ancestor of what it is
pushing) and sends that packfile upstream, where the server either stores it
on disk and builds an index for it, or unpacks it (if there aren't many objects
in it)

通过git和ssh协议推送数据(pushing data)是相似的, 但是更简单. 客户端发出一个"receive-pack"的请求, 如果客户端有访问权限, 那么服务器就返回当前引用的所有SHA串值(ref head shas). 客户端收到响应后, 计算出服务器需要的所有数据或对象, 再做成一个打包文件(packfile)传送给服务器. 服务器收到后要么就把它们存储到硬盘上再建立索引, 或是只把它解压(如果里面的对象不多的话).

This entire process is accomplished through the linkgit:git-send-pack[1] command
on the client, which is invoked by linkgit:git-push[1] and the 
linkgit:git-receive-pack[1] command on the server side, which is invoked by 
the ssh connect process or git daemon (if it's an open push server).

在这整个推数据的流程中, 客户端通过 linkgit:git-push[1] 命令调用:linkgit:git-sendpack[1]命令, 服务器端通过"ssh连接进程"或是"git服务器"来调用:linkgit:git-receive-pack 命令来完成整个操作.
