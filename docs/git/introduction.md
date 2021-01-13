# Git使用

## 基础知识

### 容器

* 本地仓库
* 远程仓库
* 暂存区

### 分支

* 远程分支

* 本地分支
  
### 操作

* 克隆
* 提交
* 查看
* 合并

### 属性

* 文件状态
* 历史记录

## 安装配置

1. 下载[git](https://git-scm.com  "git下载地址")
2. 配置用户名和邮箱

    ```git
    git config --global user.name "username"
    git config --global user.email "useremail@mail.com"
    ```

## 常用命令

### 操作本地命令

克隆代码到本地仓库
`git clone http://github.com/app/git-tutorial.git`

创建新的分支
 `git branch new-feature`

创建本地仓库的所有分支
`git branch -v`

切换分支
`git checkout new-feature`

查看分支状态
```git status```

合并分支
`git merge new-feature`

查看本地和远程分支
`git branch -a`

查看冲突文件
`git diff`

删除本地分支
`git branch -d branch-name`

### 操作远程命令

删除远程分支
```git remote remove origin```

`git push -d origin branch-name`

查看当前项目的远程分支信息

```git remote -v```

给当前项目添加一个新的远程仓库地址

```git remote add new_origin http://git.github.com/group/repo.git```

## git stash 和 git tag
