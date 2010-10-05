## Git Hooks ##

Hooks are little scripts you can place in $GIT_DIR/hooks directory to trigger
action at certain points. When git-init is run, a handful example hooks are 
copied in the hooks directory of the new repository, but by default they are 
all disabled. To enable a hook, rename it by removing its .sample suffix.

钩子(hooks)是一些在"$GIT-DIR/hooks"目录的脚本, 在被特定的事件(certain points)触发后被调用. 当"git init"命令被调用后, 一些非常有用的示例钩子文件(hooks)被拷到新仓库的hooks目录中; 但是在默认情况下这些钩子(hooks)是不生效的. 把这些钩子文件(hooks)的".sample"文件名后缀去掉就可以使它们生效了.

### applypatch-msg ###

    GIT_DIR/hooks/applypatch-msg
    
This hook is invoked by git-am script. It takes a single parameter, the name 
of the file that holds the proposed commit log message. Exiting with non-zero
status causes git-am to abort before applying the patch.

当'git-am'命令执行时，这个钩子就被调用。它只有一个参数：就是存有提交消息(commit log message)的文件的名字。如果钩子的执行结果是非零，那么补丁(patch)就不会被应用(apply)。

The hook is allowed to edit the message file in place, and can be used to 
normalize the message into some project standard format (if the project has one).
It can also be used to refuse the commit after inspecting the message file.
The default applypatch-msg hook, when enabled, runs the commit-msg hook, if the
latter is enabled.

这个钩子用于在其它地方编辑提交消息，并且可以把这些消息规范成项目的标准格式(如果项目些类的标准的话)。它也可以在分析(inspect)完消息文件后拒绝此次提交(commit)。在默认情况下，当 applypatch-msg 钩子被启用时。。。。



()

### pre-applypatch ###

    GIT_DIR/hooks/pre-applypatch

This hook is invoked by git-am. It takes no parameter, and is invoked after the
patch is applied, but before a commit is made.
If it exits with non-zero status, then the working tree will not be committed
after applying the patch.

当'git-am'命令执行时，这个钩子就被调用。它没有参数，并且是在一个补丁(patch)被应用且在完成提交(commit)前被调用。如果钩子的执行结果是非零，那么刚才应用的补丁(patch)就不会被提交。

It can be used to inspect the current working tree and refuse to make a commit 
if it does not pass certain test.
The default pre-applypatch hook, when enabled, runs the pre-commit hook, if the
latter is enabled.

它用于检查当前的工作树，当提交的补丁不能通过特定的测试就拒绝将它提交(commit)进仓库。
()

### post-applypatch ###

    GIT_DIR/hooks/post-applypatch
    
This hook is invoked by 'git-am'.  It takes no parameter,
and is invoked after the patch is applied and a commit is made.

当'git-am'命令执行时，这个钩子就被调用。它没有参数，并且是在一个补丁(patch)被应用且在完成提交(commit)情况下被调用。

This hook is meant primarily for notification, and cannot affect
the outcome of 'git-am'.

这个钩子的主要用途是通知提示(notification)，它并不会影响'git-am'的执行和输出。

### pre-commit ###
 	
    GIT_DIR/hooks/pre-commit

This hook is invoked by 'git-commit', and can be bypassed
with `\--no-verify` option.  It takes no parameter, and is
invoked before obtaining the proposed commit log message and
making a commit.  Exiting with non-zero status from this script
causes the 'git-commit' to abort.

这个钩子被 'git-commit' 命令调用, 而且可以通添加`\--no-verify` 参数来跳过。它没有参数，在得到提交消息和开始提交前被调用。如果钩子执行结果是非零，那么 'git-commit' 命令就会中止执行。

The default 'pre-commit' hook, when enabled, catches introduction
of lines with trailing whitespaces and aborts the commit when
such a line is found.

当默认的'pre-commit'钩子开启时，如果它发现提交消息的开头(introduction)都是空白行，那么就会中止此次提交。


All the 'git-commit' hooks are invoked with the environment
variable `GIT_EDITOR=:` if the command will not bring up an editor
to modify the commit message.


Here is an example of a Ruby script that runs RSpec tests before allowing a commit.

下面是一个运行 Rspec 测试的 Ruby 脚本，如果没有通过这个测试，那么不允许提交(commit)。
	ruby  
	html_path = "spec_results.html"  
	`spec -f h:#{html_path} -f p spec` # run the spec. send progress to screen. save html results to html_path  

	# find out how many errors were found  
	html = open(html_path).read  
	examples = html.match(/(\d+) examples/)[0].to_i rescue 0  
	failures = html.match(/(\d+) failures/)[0].to_i rescue 0  
	pending = html.match(/(\d+) pending/)[0].to_i rescue 0  

	if failures.zero?  
	  puts "0 failures! #{examples} run, #{pending} pending"  
	else  
	  puts "\aDID NOT COMMIT YOUR FILES!"  
	  puts "View spec results at #{File.expand_path(html_path)}"  
	  puts  
	  puts "#{failures} failures! #{examples} run, #{pending} pending"  
	  exit 1  
	end

    
### prepare-commit-msg ###

    GIT_DIR/hooks/prepare-commit-msg

This hook is invoked by 'git-commit' right after preparing the
default log message, and before the editor is started.

当'git-commit'命令执行时：在编辑器(editor)启动前，默认提交消息准备好后，这个钩子就被调用。


It takes one to three parameters.  The first is the name of the file
that the commit log message.  The second is the source of the commit
message, and can be: `message` (if a `-m` or `-F` option was
given); `template` (if a `-t` option was given or the
configuration option `commit.template` is set); `merge` (if the
commit is a merge or a `.git/MERGE_MSG` file exists); `squash`
(if a `.git/SQUASH_MSG` file exists); or `commit`, followed by
a commit SHA1 (if a `-c`, `-C` or `\--amend` option was given).

它有三个参数。第一个是提交消息文件的名字。第二个是提交消息的来源，它可以是：().

If the exit status is non-zero, 'git-commit' will abort.

如果钩子的执行結果是非零的话，那么'git-commit'命令就会被中止执行。

The purpose of the hook is to edit the message file in place, and
it is not suppressed by the `\--no-verify` option.  A non-zero exit
means a failure of the hook and aborts the commit.  It should not
be used as replacement for pre-commit hook.



The sample `prepare-commit-msg` hook that comes with git comments
out the `Conflicts:` part of a merge's commit message.


### commit-msg ###

    GIT_DIR/hooks/commit-msg

This hook is invoked by 'git-commit', and can be bypassed
with `\--no-verify` option.  It takes a single parameter, the
name of the file that holds the proposed commit log message.
Exiting with non-zero status causes the 'git-commit' to
abort.

当'git-commit'命令执行时，这个钩子被调用；也可以添加`\--no-verify`参数来跳过。它有一个参数：就是被选定的提交消息文件的名字。如这个钩子的执行結果是非零，那么'git-commit'命令就会中止执行。

The hook is allowed to edit the message file in place, and can
be used to normalize the message into some project standard
format (if the project has one). It can also be used to refuse
the commit after inspecting the message file.


The default 'commit-msg' hook, when enabled, detects duplicate
"Signed-off-by" lines, and aborts the commit if one is found.


### post-commit ###

    GIT_DIR/hooks/post-commit

This hook is invoked by 'git-commit'.  It takes no
parameter, and is invoked after a commit is made.

当'git-commit'命令执行时，这个钩子就被调用。它没有参数，并且是在一个提交(commit)完成时被调用。

This hook is meant primarily for notification, and cannot affect
the outcome of 'git-commit'.

这个钩子的主要用途是通知提示(notification)，它并不会影响'git-commit'的执行和输出。


### pre-rebase ###

    GIT_DIR/hooks/pre-rebase

This hook is called by 'git-rebase' and can be used to prevent a branch
from getting rebased.

当'git-base'命令执行时，这个钩子就被调用；主要目的是阻止那不应被rebase的分支被rebase(例如，一个已经发布的分支提交就不应被rebase)。


### post-checkout ###

    GIT_DIR/hooks/post-checkout

This hook is invoked when a 'git-checkout' is run after having updated the
worktree.  The hook is given three parameters: the ref of the previous HEAD,
the ref of the new HEAD (which may or may not have changed), and a flag
indicating whether the checkout was a branch checkout (changing branches,
flag=1) or a file checkout (retrieving a file from the index, flag=0).
This hook cannot affect the outcome of 'git-checkout'.


当'git-checkout'命令更新完整个工作树(worktree)后，这个钩子就会被调用。这个钩子有三个参数：前一个HEAD的引用(ref)，新HEAD的引用，判断一个签出是分支签出还是文件签出的标识符(分支签出＝1，文件签出＝0)。这个钩子不能影响'git-checkout'命令的输出。

This hook can be used to perform repository validity checks, auto-display
differences from the previous HEAD if different, or set working dir metadata
properties.

这个钩子可以用于仓库的一致性的检查，自动显示签出前和签出后的代码的区别，也可以用于设置目录的元数据属性。

### post-merge ###

    GIT_DIR/hooks/post-merge

This hook is invoked by 'git-merge', which happens when a 'git-pull'
is done on a local repository.  The hook takes a single parameter, a status
flag specifying whether or not the merge being done was a squash merge.
This hook cannot affect the outcome of 'git-merge' and is not executed,
if the merge failed due to conflicts.

它有一个参数：

This hook can be used in conjunction with a corresponding pre-commit hook to
save and restore any form of metadata associated with the working tree
(eg: permissions/ownership, ACLS, etc).  See contrib/hooks/setgitperms.perl
for an example of how to do this.



### pre-receive ###

    GIT_DIR/hooks/pre-receive

This hook is invoked by 'git-receive-pack' on the remote repository,
which happens when a 'git-push' is done on a local repository.
Just before starting to update refs on the remote repository, the
pre-receive hook is invoked.  Its exit status determines the success
or failure of the update.

当用户在本地仓库执行'git-push'命令时，服务器上运端仓库就会对应执行'git-receive-pack'，而'git-receive-pack'会调用 pre-receive 钩子。

This hook executes once for the receive operation. It takes no
arguments, but for each ref to be updated it receives on standard
input a line of the format:

  <old-value> SP <new-value> SP <ref-name> LF

where `<old-value>` is the old object name stored in the ref,
`<new-value>` is the new object name to be stored in the ref and
`<ref-name>` is the full name of the ref.
When creating a new ref, `<old-value>` is 40 `0`.

If the hook exits with non-zero status, none of the refs will be
updated. If the hook exits with zero, updating of individual refs can
still be prevented by the <<update,'update'>> hook.

Both standard output and standard error output are forwarded to
'git-send-pack' on the other end, so you can simply `echo` messages
for the user.

If you wrote it in Ruby, you might get the args this way:

	ruby
	rev_old, rev_new, ref = STDIN.read.split(" ")

Or in a bash script, something like this would work:
	
	#!/bin/sh
	# <oldrev> <newrev> <refname>
	# update a blame tree
	while read oldrev newrev ref
	do
		echo "STARTING [$oldrev $newrev $ref]"
		for path in `git diff-tree -r $oldrev..$newrev | awk '{print $6}'`
		do
		  echo "git update-ref refs/blametree/$ref/$path $newrev"
		  `git update-ref refs/blametree/$ref/$path $newrev`
		done
	done

    
### update ###

    GIT_DIR/hooks/update

This hook is invoked by 'git-receive-pack' on the remote repository,
which happens when a 'git-push' is done on a local repository.
Just before updating the ref on the remote repository, the update hook
is invoked.  Its exit status determines the success or failure of
the ref update.

当用户在本地仓库执行'git-push'命令时，服务器上运端仓库就会对应执行'git-receive-pack'，而'git-receive-pack'会调用 update 钩子。
钩子的执行结果(exit status)()

The hook executes once for each ref to be updated, and takes
three parameters:

每更新一个引用(ref)，钩子就就被调用一次，并且使用三个参数:

 - the name of the ref being updated,
 - the old object name stored in the ref,
 - and the new objectname to be stored in the ref.

A zero exit from the update hook allows the ref to be updated.
Exiting with a non-zero status prevents 'git-receive-pack'
from updating that ref.

如果 update hook 的执行结果是“0”，那么引用(ref)就会被更新。如果执行结果是非零，那么’git-receive-pack'就不会更新这个引用(ref)。

This hook can be used to prevent 'forced' update on certain refs by
making sure that the object name is a commit object that is a
descendant of the commit object named by the old object name.
That is, to enforce a "fast forward only" policy.


It could also be used to log the old..new status.  However, it
does not know the entire set of branches, so it would end up
firing one e-mail per ref when used naively, though.  The
<<post-receive,'post-receive'>> hook is more suited to that.

Another use suggested on the mailing list is to use this hook to
implement access control which is finer grained than the one
based on filesystem group.

在邮件列表(mailing list)上讲了另外一种用法：用这个 update hook 实现细粒度(finer grained)权限控制。

Both standard output and standard error output are forwarded to
'git-send-pack' on the other end, so you can simply `echo` messages
for the user.

钩子(hook)的标准输出和标准错误输出(stdout & stderr)都会通'git-send-pack'转发给客户端。你可以把这个信息也显示给用户。

The default 'update' hook, when enabled--and with
`hooks.allowunannotated` config option turned on--prevents
unannotated tags to be pushed.

当默认的 update hook 被启用，且`hooks.allowunannotated`选项被打开时，那么没有注释(unannotated)标签就不能被推送到服务器上。

### post-receive ###

    GIT_DIR/hooks/post-receive
    
This hook is invoked by 'git-receive-pack' on the remote repository,
which happens when a 'git-push' is done on a local repository.
It executes on the remote repository once after all the refs have
been updated.

当用户在本地仓库执行'git-push'命令时，服务器上运端仓库就会对应执行'git-receive-pack'。在所有远程仓库的引用(ref)都更新后，post-update 就会被调用。

This hook executes once for the receive operation.  It takes no
arguments, but gets the same information as the
<<pre-receive,'pre-receive'>>
hook does on its standard input.

This hook does not affect the outcome of 'git-receive-pack', as it
is called after the real work is done.

This supersedes the <<post-update,'post-update'>> hook in that it gets
both old and new values of all the refs in addition to their
names.

Both standard output and standard error output are forwarded to
'git-send-pack' on the other end, so you can simply `echo` messages
for the user.

The default 'post-receive' hook is empty, but there is
a sample script `post-receive-email` provided in the `contrib/hooks`
directory in git distribution, which implements sending commit
emails.


### post-update ###

    GIT_DIR/hooks/post-update
    
This hook is invoked by 'git-receive-pack' on the remote repository,
which happens when a 'git-push' is done on a local repository.
It executes on the remote repository once after all the refs have
been updated.

当用户在本地仓库执行'git-push'命令时，服务器上运端仓库就会对应执行'git-receive-pack'。在所有远程仓库的引用(ref)都更新后，post-update 就会被调用。

It takes a variable number of parameters, each of which is the
name of ref that was actually updated.



This hook is meant primarily for notification, and cannot affect
the outcome of 'git-receive-pack'.

这个钩子的主要用途是通知提示(notification)，它并不会影响'git-receive-pack'的输出。

The 'post-update' hook can tell what are the heads that were pushed,
but it does not know what their original and updated values are,
so it is a poor place to do log old..new. The
<<post-receive,'post-receive'>> hook does get both original and
updated values of the refs. You might consider it instead if you need
them.


When enabled, the default 'post-update' hook runs
'git-update-server-info' to keep the information used by dumb
transports (e.g., HTTP) up-to-date.  If you are publishing
a git repository that is accessible via HTTP, you should
probably enable this hook.

Both standard output and standard error output are forwarded to
'git-send-pack' on the other end, so you can simply `echo` messages
for the user.


### pre-auto-gc ###

    GIT_DIR/hooks/pre-auto-gc

This hook is invoked by 'git-gc --auto'. It takes no parameter, and
exiting with non-zero status from this script causes the 'git-gc --auto'
to abort.

当调用'git-gc --auto'命令时，这个钩子(hook)就会被调用。它没有调用参数，如果钩子的执行結果是非零的话，那么'git-gc --auto'命令就会被中止执行。

### References ###
### 参考 ###

[Git Hooks](http://www.kernel.org/pub/software/scm/git/docs/githooks.html)
* http://probablycorey.wordpress.com/2008/03/07/git-hooks-make-me-giddy/