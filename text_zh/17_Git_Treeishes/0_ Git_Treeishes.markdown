## Git Treeishes ##
## Git树名 ##

There are a number of ways to refer to a particular commit or tree other
than spelling out the entire 40-character sha.  In Git, these are referred
to as a 'treeish'.

不用40个字节长的SHA串来表示一个提交(commit)或是其它git对象, 有很多种表示方法.　在Git里,它就叫'树名'(treeish).

译者注:我目前没有想到更好的中文名字,就先叫'树名'.
 
### Partial Sha ###
### Sha短名 ###

If your commit sha is '<code>980e3ccdaac54a0d4de358f3fe5d718027d96aae</code>', git will 
recognize any of the following identically:

如果你的一个提交(commit)的sha名字是 '<code>980e3ccdaac54a0d4de358f3fe5d718027d96aae</code>', git会把下面的串视为等价的.

	980e3ccdaac54a0d4de358f3fe5d718027d96aae
	980e3ccdaac54a0d4
	980e3cc

As long as the partial sha is unique - it can't be confused with another
(which is incredibly unlikely if you use at least 5 characters), git will
expand a partial sha for you.

只要你的‘sha短名’(Partial Sha)是不重复的(unique)，不影响到其它的(如果你使用了5个字节是很难重复的)，那么git就会把‘sha短名’(Partial Sha)自动补全.

### Branch, Remote or Tag Name ###
### 分支, Remote 或 标签 ###

You can always use a branch, remote or tag name instead of a sha, since they
are simply pointers anyhow.  If your master branch is on the 980e3 commit and
you've pushed it to origin and have tagged it 'v1.0', then all of the following
are equivalent:

你可以使用分支,remote或标签名来代替SHA串名, 它们只是指向某个对象的指针. 假设你的master分支现在提交(commit):'980e3'上, 现在把它推送(push)到origin上而且把它命名为标签'v1.0', 那么下面的串都会被git视为等价的:

	980e3ccdaac54a0d4de358f3fe5d718027d96aae
	origin/master
	refs/remotes/origin/master
	master
	refs/heads/master
	v1.0
	refs/tags/v1.0
	
Which means the following will give you identical output:

这意味着你执行下面的两条命令会有同样的输出:

	$ git log master
	
	$ git log refs/tags/v1.0
	
### Date Spec ###
### 日期标识符 ###

The Ref Log that git keeps will allow you to do some relative stuff locally, 
such as: 

Git的引用日志(Ref Log)可以让你做一些‘相对'查询操作:

	master@{yesterday}

	master@{1 month ago}
	
Which is shorthand for 'where the master branch head was yesterday', etc. Note
that this format can result in different shas on different computers, even if
the master branch is currently pointing to the same place.

上面的第一条命令是:'master分支的昨天状态(head)的缩写‘. 注意: 即使在两个有相同master分支指向的仓库上执行这条命令, 但是如果这个两个仓库在不同机器上,　那么执行结果也很可能会不一样.

### Ordinal Spec ###
### 顺序标识符 ###

This format will give you the Nth previous value of a particular reference.
For example:

这种格式用来表达某点前面的第N个提交(ref).

	master@{5}

will give you the 5th prior value of the master head ref.

上面的表达式代表着master前面的第5个提交(ref).
	
### Carrot Parent ###
### 多个父对象 ###

This will give you the Nth parent of a particular commit.  This format is only
useful on merge commits - commit objects that have more than one direct parent.

这能告诉你某个提交的第N个嫡父提交(parent).这种格式在合并提交(merge commits)时特别有用, 这样就可以使用提交对象(commit object)有多于一个直接父对象(direct parent).

译者注:假设master是由a和b两个分支合并的,那么master^1是指分支a,master^2就是指分支b.

	master^2
	
	
### Tilde Spec ###
### 波浪号 ###

The tilde spec will give you the Nth grandparent of a commit object.  For example,

波浪号用来标识一个提交对象(commit object)的第N级嫡父对象(Nth grandparent). 例如:

	master~2
	
will give us the first parent of the first parent of the commit that master 
points to.  It is equivalent to:

就代表master所指向的提交对象的第一个父对象的第一个父对象(译者:你可以理解成是直系爷爷:)). 它和下面的这个表达式是等价的:

	master^^

You can keep doing this, too.  The following specs will point to the same commit:

你也可以这个些‘标识符'(spec)叠加起来, 下面这个3个表达式都是指向同一个提交(commit):

	master^^^^^^
	master~3^~2
	master~6

### Tree Pointer ###
### 树对象指针 ###

This disambiguates a commit from the tree that it points to.  If you want the 
sha that a commit points to, you can add the '^{tree}' spec to the end of it.

如果大家对第一章还有印象的话, 就记得提交对象(commit object)是指向一个树对象(tree object)的. 假如你要得一个提交对象(commit object)指向的树对象(tree object)的sha串名, 你就可以在‘树名'的后面加上'^{tree}'来得到它:

	master^{tree}

### Blob Spec ###

If you want the sha of a particular blob, you can add the blob path at the
end of the treeish, like so:

如果你要某个二次制对象(blob)的sha串名,你可以在'树名'(treeish)后添加二次制对象(blob)对应的文件路径来得到它.
 
	master:/path/to/file


	
### Range ###
### 区间 ###

Finally, you can specify a range of commits with the range spec.  This will
give you all the commits between 7b593b5 and 51bea1 (where 51bea1 is most recent),
excluding 7b593b5 but including 51bea1:

最后, 你可以用".."来指两个提交(commit)之间的区间. 下面的命令会给你在"7b593b5" 和"51bea1"之间除了"7b593b5外"的所有提交(commit)(51bea1是最近的提交).


	7b593b5..51bea1

This will include every commit *since* 7b593b:

这会包括所有 *从* 7b593b开始的提交(commit).
译者注: 相当于 7b593b..HEAD

	7b593b.. 
	
	