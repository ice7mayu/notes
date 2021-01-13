# Stash

将本地的改动暂时保存，以便于本地代码以一个上一次提交记录的状态去merge其他分支、拉取远程代码、修改bug上线等。

- 本地修改文件已加入暂存区（文件状态为tracked）
  
```bash
$ git stash push -m "stash only tracked files"
Saved working directory and index state On dev: stash only tracked files
```
  
- 本地修改文件未加入暂存区（文件状态为untracked）  
需要加上参数 `-u|--include-untracked`:

```bash
$ git stash push -u -m "stash both tracked and untracked files"
Saved working directory and index state On dev: stash both tracked and untracked files
```
  
- 查看stash区域有哪些快照

```bash
$ git stash list
stash@{0}: On dev: Your stash message
```

- 弹出某次保存的快照  
不加索引默认弹出最后一次保存的快照：

```bash
$ git stash pop
Dropped refs/stash@{0} (1665772fc92d2aa04befe5009bfdc67f24401d1f)
```

```bash
$ git stash pop n
Dropped refs/stash@{n} (1665772fc92d2aa04befe5009bfdc67f24401d1f)
```

表示弹出第n次保存的快照  
注意：0表示最近一次，1表示最近第二次，以此类推

- 弹出某次保存的快照并删除stash区域的快照

```bash
$ git stash pop 1
Dropped refs/stash@{1} (ff65772fc92d2aa04befe5009bfdc67f24401d2b)
```
  
- 删除stash区域的快照

```bash
$ git stash drop 1
Dropped refs/stash@{1} (751b5897bf68425080462d583763807139a8a4ae)
```
  
- 删除 stash 空间的全部快照

```bash
git stash clear
```
