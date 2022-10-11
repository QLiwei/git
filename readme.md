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
git show v1.x
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

### 2.2分支开发工作流

```
长期分支
master
develop
next 的平行分支
proposed（建议） 或 pu: proposed updates（建议更新）分支
主题分支
主题分支是一种短期分支，它被用来实现单一特性或其相关工作
```

### 2.3远程分支

Git 的 `clone` 命令会为你自动将其命名为 `origin`，拉取它的所有数据， 创建一个指向它的 `master` 分支的指针，并且在本地将其命名为 `origin/master`。 Git 也会给你一个与 origin 的 `master` 分支在指向同一个地方的本地 `master` 分支，这样你就有工作的基础。

```
显式地获得远程引用的完整列表
git ls-remote <remote>
获得远程分支的更多信息
git remote show <remote>
远程仓库中的位置以 <remote>/<branch> 的形式命名

远程仓库同步数据
git fetch <remote> 
添加远程分支
git remote add <remote> url

推送
git push <remote> <branch>

git push origin serverfix
git push origin serverfix:serverfix
serverfix 分支名字展开为 refs/heads/serverfix:refs/heads/serverfix
origin serverfix:awesomebranch 来将本地的 serverfix 分支推送到远程仓库上的 awesomebranch 分支

git fetch origin 
将这些工作合并到当前所在的分支
git merge origin/serverfix
创建用于工作的本地分支，并且起点位于 origin/serverfix
git checkout -b serverfix origin/serverfix

跟踪分支

自动地识别去哪个服务器上抓取、合并到哪个分支
git pull
当克隆一个仓库时，它通常会自动地创建一个跟踪 origin/master 的 master 分支
git checkout -b <branch> <remote>/<branch>
git checkout --track origin/serverfix

拉取
git pull 的魔法经常令人困惑所以通常单独显式地使用 fetch 与 merge 命令会更好一些。

删除远程分支
git push origin --delete serverfix
```

**“origin” 并无特殊含义**

远程仓库名字 “origin” 与分支名字 “master” 一样，在 Git 中并没有任何特别的含义一样。 同时 “master” 是当你运行 `git init` 时默认的起始分支名字，原因仅仅是它的广泛使用， “origin” 是当你运行 `git clone` 时默认的远程仓库名字。 如果你运行 `git clone -o booyah`，那么你默认的远程分支名字将会是 `booyah/master`。

**如何避免每次输入密码**

如果你正在使用 HTTPS URL 来推送，Git 服务器会询问用户名与密码。 默认情况下它会在终端中提示服务器是否允许你进行推送。

如果不想在每一次推送时都输入用户名与密码，你可以设置一个 “credential cache”。 最简单的方式就是将其保存在内存中几分钟，可以简单地运行 `git config --global credential.helper cache` 来设置它。

### 2.4变基

**变基使得提交历史更加整洁**

 你在查看一个经过变基的分支的历史记录时会发现，尽管实际的开发工作是并行的， 但它们看上去就像是串行的一样，提交历史是一条直线没有分叉。

在 Git 中整合来自不同分支的修改主要有两种方法：`merge` 以及 `rebase`

你可以提取在 `C4` 中引入的补丁和修改，然后在 `C3` 的基础上应用一次。 在 Git 中，这种操作就叫做 **变基（rebase）**。

```
git checkout experiment
git rebase master
git checkout master
git merge experiment
```

```
git rebase --onto master server client
取出 client 分支，找出它从 server 分支分歧之后的补丁， 然后把这些补丁在 master 分支上重放一遍，让 client 看起来像直接基于 master 修改一样”。

git checkout master
git merge client

将主题分支变基到目标分支
git rebase <basebranch> <topicbranch>


git pull --rebase
git fetch
git rebase teamone/master
```

**变基的风险**

呃，奇妙的变基也并非完美无缺，要用它得遵守一条准则：

**如果提交存在于你的仓库之外，而别人可能基于这些提交进行开发，那么不要执行变基。**

如果你遵循这条金科玉律，就不会出差错。 否则，人民群众会仇恨你，你的朋友和家人也会嘲笑你，唾弃你。

变基操作的实质是丢弃一些现有的提交，然后相应地新建一些内容一样但实际上不同的提交。 如果你已经将提交推送至某个仓库，而其他人也已经从该仓库拉取提交并进行了后续工作，此时，如果你用 `git rebase` 命令重新整理了提交并再次推送，你的同伴因此将不得不再次将他们手头的工作与你的提交进行整合，如果接下来你还要拉取并整合他们修改过的提交，事情就会变得一团糟。