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


