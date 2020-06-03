## git 操作指南
> [] 表示是可以修改的变量名。用户自己定义  
> () 中的内容表示非必填内容

### 普通流程
1. `git clone (-b [branchName]) [url|personalUrl] ([localPath])`
> 省略 `-b [branchName]` 将会克隆所有分支，进去后默认 master 分支  
> 省略 `[localPath]` 将会克隆到运行命令的同级路径下

1. `git remote add [name] [mainUrl]`
> 添加主仓库地址别名  
> `git remote -v` 查看所有远程别名信息

1. `git checkout [branchName]`
> 切换到需要开发的分支下  
> `git branch` 查看所有本地检出的分支名

1. `git add .`
> 将所有更改添加到暂存区  
> `git status` 查看状态

1. `git commit -m [message]`
> 添加提交信息

1. `git push (origin [branch])`
> 推送到远程仓库（一般是个人远程仓库）


### 常用命令

1. 开发前和 push 前一般更新下本地代码  
	- `git pull [name] [branchName]`
	> 相当于 `git fetch` 和 `git merge [personalUrl]`

1. 冲突解决
	1. `git stash` 保存当前工作进度
	2. `git pull [name] [branchName]` 同步
	3. `git stash pop` 恢复最新的进度到工作区
	4. 解决冲突后 `git push`
 
1. 合并分支
	1. `git checkout [A_branchName]` 检出到合并后的分支上
	1. `git merge [B_branchName]` 合并 B 到 A
 
1. 创建新分支
	1. `git branch [branchName]` 创建新分支
	2. `git checkout -b [branchName]` 创建新分支并检出到该分支
 
1. 在还没有push到远程时。 回滚到之前某一 commit
	1. `git log` 查看需要恢复到某个commit时的id
	2. `git reset --hard [commitID]` 回归到该ID对应的状态
 
1. 修改提交信息
	1. `git commit --amend`
