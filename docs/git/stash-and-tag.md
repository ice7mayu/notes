# Git stash and tag

## Git stash

### 什么是 stash

stash 能够将修改的代码临时保存起来, 从而恢复工作目录到上一次提交的状态.
而不需要创建临时分支, 也不需要提交未完成的代码.

stash 在本地磁盘有独立的存放空间, 但只能保留在本地, 不能同步到远程.

每一次 stash 都是独立的实体, 有独立的存档信息, 所以可以多次 stash,
也可以从 stash list 中挑选不同的存档来恢复到工作目录.

可以有效由于临时任务所带来的分支或者提交的困扰.

### 什么时候需要用到 stash

1. 工作过程中, 需要从 upstream 拉取更新
2. 工作过程中, 需要合并其他分支
3. 工作过程中, 突然要临时修改其他bug

### Git Bash 中如何操作

`stash push`

只将 tracked 的文件保存起来, 包括加入暂存区的和未加入暂存区的.
而不包括 untracked 的文件:

```bash
$ git stash push -m "stash only tracked files"
Saved working directory and index state On dev: stash only tracked files
```

如果想包括 untracked 的文件, 需要加上参数 `-u|--include-untracked`:

```bash
$ git stash push -u -m "stash both tracked and untracked files"
Saved working directory and index state On dev: stash both tracked and untracked files
```

stash 之后的工作区, 就会恢复到未修改的状态, 也就是最近一次提交的状态, 即 HEAD 所在的提交历史.

`stash list`

查看 stash 中都保存了哪些快照:

```bash
$ git stash list
stash@{0}: On dev: Your stash message
```

`stash pop`

从 stash 中弹出最近的一次(即索引为 0 的)快照:

```bash
$ git stash pop
Dropped refs/stash@{0} (1665772fc92d2aa04befe5009bfdc67f24401d1f)
```

也可以在 `stash pop` 后加上具体某一次 stash 的索引 `[1|stash@{1}]`:

```bash
$ git stash pop 1
Dropped refs/stash@{1} (ff65772fc92d2aa04befe5009bfdc67f24401d2b)
```

弹出的同时也会从 stash 空间中删除本次快照

`stash apply`

如果只想从 stash 空间中应用某一次快照, 而不从 stash 空间中删除, 可以用 `stash apply`:

```bash
git stash apply 0
```

`stash drop`

删除 stash 空间的某一个快照

```bash
$ git stash drop 1
Dropped refs/stash@{1} (751b5897bf68425080462d583763807139a8a4ae)
```

删除 stash 空间的全部快照

```bash
git stash clear
```

### Pycharm 中如何操作

查看 stash list 中的某一个快照: **VCS > Git > UnStash Changes...**

在 Pycharm 中只用来查看 stash 中对文件的修改, 其他操作尽量命令行哈.

## Git tag

Tag 标签, 用来给特定的提交历史(commit hash)起一个有意义的名称, 表示软件达到了某一可交付的状态.
通常用语义化版本来命名标签, 例如: v0.1, v2.3.4 等.

一般是软件通过测试后, 代码合并到 `master` 分支后, 再进行打标签.

在Git中分为轻量级标签(lightweight tag)和注解标签(Annotated tag)两种.

轻量级的标签 (lightweight tag):

只是给某一个 commit hash 起一个别名而已, 不包含其他信息:

```bash
git tag v0.1
```

以后可以通过这个标签(别名)来创建新的分支, 例如, 要基于v0.1版本创建一个分支并修复一个bug:

```bash
$ git checkout -b fix-bug v0.1
Switched to a new branch 'fix-bug'
```

带注解的标签:

包含了标签创建的时间, 创建人, 邮箱, 标签信息, 签名信息等, 并且必须包含标签的信息:

```bash
git tag -a v1.0 -m "版本信息"
```

查看标签:

```bash
git tag -l
```

如果想查看标签信息需要加上 `-n`, 例如, 查看标签信息的前5行:

```bash
$ git tag -l -n5
v1.0            version 1.0
```

将本地的某一个标签 push 到远程仓库:

```bash
git push origin v1.0
```

PS. tag 标签不需要 track 远程仓库的改变, 所以这里的 push 后面不需要 `-u`.

将本地所有标签 push 到远程:

```bash
git push --tags
```

删除本地标签:

```bash
$ git tag -d v1.0
Deleted tag 'v1.0' (was bcac848)
```

删除远程标签:

```bash
$ git push -d origin v1.0
To git.github.com:username/learn-git.git
 - [deleted]         v1.0
```

----
Done
