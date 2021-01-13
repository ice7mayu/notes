# Git squash merge

## 什么是 squash merge

在执行 `git merge` 合并分支的时候, 传入 `--squash` 参数,
把目标分支中多次提交的内容合并在一起并添加到 `staging area`(`index`) 暂存区,
不自动执行合并操作, 而是等待下一次手动提交, 从而达到
将目标分支的多次提交挤压合并为一次提交的效果.

## 什么情况下使用

1. 新建一个分支用于开发新功能, 在开发过程中, 需要多次提交到功能分支, 最终合并到主分支时, 只关心最终结果, 而并不关心中间提交的历史.
2. 创建一个分支用于修改bug, 反复修改需要多次提交, 最终只关心修复结果, 而不关心中间提交的历史.

Pros:

可以使提交历史看起来更整洁, 避免中途多余的提交造成提交历史冗长.

Cons:

由于合并过程中是由合并者提交一次来完成的, 因此会丢掉目标分支的提交历史和提交者信息.

## Git Bash 命令

新建一个 `new-features` 分支用于实现 2 个新功能, 这两个新功能按 2 次提交:

```bash
# Create a new-features branch
$ git checkout -b new-features
Switched to a new branch 'new-features'

# Implement new feature 1
$ echo "Add new feature in log1" >> log1.txt
$ git commit -am "Add new feature in log1"

The file will have its original line endings in your working directory
[new-features e42c5a7] Add new feature in log1
 1 file changed, 1 insertion(+)

# Implement new feature 2
$ echo "Add new feature in log2" >> log2.txt
$ git add log2.txt
$ git commit -m "Add new feature in log2"

[new-features 979800a] Add new feature in log2
 1 file changed, 1 insertion(+)
 create mode 100644 log2.txt
```

查看当前分支有 2 次提交历史:

```bash
$ git log --oneline -n3

979800a (HEAD -> new-features) Add new feature in log2
e42c5a7 Add new feature in log1
6290e23 (tag: v0.2, origin/dev, dev) Ignore idea dir
```

此时 2 个新功能都实现了, 需要合并到 dev 分支中, 但是对于 dev 分支来说,
只需要知道这 2 个功能都实现了就可以了, 而不关心具体是提交了多少次才实现的:

```bash
# Switch to dev branch
$ git checkout dev
Switched to branch 'dev'
Your branch is up to date with 'origin/dev'.

# Perform a squash merge
$ git merge --squash new-features
Updating 6290e23..979800a
Fast-forward
Squash commit -- not updating HEAD
 log1.txt | 1 +
 log2.txt | 1 +
 2 files changed, 2 insertions(+)
 create mode 100644 log2.txt
```

此时会将 `new-features` 的多次修改统一加在暂存区中, 而不会自动合并:

```bash
# View the status of the staging area(index)
$ git status
On branch dev
Your branch is up to date with 'origin/dev'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   log1.txt
        new file:   log2.txt
```

检查过所有的修改, 并确保无误, 进行手动提交:

```bash
$ git commit -m "Implement all of the new features"
[dev f666b12] Implement all of the new features
 2 files changed, 2 insertions(+)
 create mode 100644 log2.txt
```

查看合并历史, 只有 1 条提交信息(`f666b12`):

```bash
$ git log --oneline -n5
f666b12 (HEAD -> dev) Implement all of the new features
6290e23 (tag: v0.2, origin/dev) Ignore idea dir
5b9118e (tag: v0.1) Add log1
b6a6590 (origin/master, origin/HEAD, master) Initial commit
```

----
Done
