## 1.git 基础学习

### 1.1获取git仓库

```
git init

git add filename
git commit -m "commit info"
git commit -m
git commit --amend

克隆仓库
git clone <url>
```

### 1.2文件状态

------------- 未追踪
untracked:未追踪状态
------------- 已追踪
unmodified:未修改
modified:修改过
staged:暂存区

```
查看状态
git status
状态简览
git status -s

查看工作目录和暂存区差异
git diff filename
暂存区和commit区差异
git diff --staged
```

### 1.3撤销操作

```

```

### 1.4标签

```
查看标签
git tag
打标签
附注标签
git tag -a v1.x -m ""
轻量标签
git tag v1.x-lw
后期打标签
git log --pretty=oneline
git tag -a v1.2 9fceb02
共享标签
git push origin v1.x
git push origin --tags
查看标签信息
git show tag v1.x
删除标签
git tag -d v1.x
git push <remote> :refs/tags/<tagname>
```

## 2.分支

HEAD 分支 指向当前分支

```
查看分支
git branch
创建分支
git branch <分支名>
切换分支
git checkout <分支名>
创建并切换到分支
git branch -a <分支名>
删除分支
git branch -d <分支名>
合并分支
git merge <分支名>
解决冲突
git status 
修改文件冲突
git add <file>
git commit
```

### 2.1分支管理

```
查看分支
git branch
查看每一个分支的最后一次提交
git branch -v
查看哪些分支已经合并到当前分支
git branch --merged
查看哪些分支没有合并到当前分支
git branch --no-merged
删除分支
git branch -d <分支名>
存在未合并的工作 可以使用 -D 选项强制删除它
git branch -D <分支名>
```

