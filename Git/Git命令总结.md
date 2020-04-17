## 1.初始化配置

`git config --global user.name "Your Name"`

`git config --global user.email "email@example.com"`



## 2.初始化repository版本库

`git init`



## 3.文件添加到暂存区提交到版本库

`git add filename`

`git commit -m <message>`

`git commit --amend`：修改提交到版本库时的message信息。



## 4.查看文件状态

`git status`



## 5.查看文件修改的内容

`git diff filename`



## 6.版本退回

`git reset --hard commit_id`



## 7.查看提交历史与命令历史

`git log`：提交历史

`git reflog`：命令历史



## 8.撤销修改

`git checkout -- filename`：撤销工作区修改，让这个文件回到最近一次`git commit`或`git add`时的状态。（场景1）

`git reset HEAD filename`：改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD filename`，就回到了场景1，第二步按场景1操作。



## 9.删除文件

`git rm filename`

`git commit -m <message>`



## 10.撤销本地删除，版本库中还保留

`git checkout -- filename`：返回到最近的`git commit`状态。



## 11.创建SSH Key

` ssh-keygen -t rsa -C "youremail@example.com"`



## 12.添加、删除、重命名远程仓库

`git remote add <远程仓库名字> git@github.com:RawOnion/learngit.git`：添加某个远程仓库到本地

`git remote rm <远程仓库名字>`：删除本地添加的远程仓库

`git remote rename <旧远程仓库名字> <新远程仓库名字>`：修改某个远程仓库在本地的简称



## 13.操作远程仓库命令

`git push -u origin master`：本地仓库内容推送到远程仓库，第一次需要把本地的`master`分支和远程的`master`分支关联起来。

` git push origin master`：以后的简化命令，推送到远程`master`分支。

`git push <远程仓库本地别名> <远程仓库分支名>`：本地内容推送到远程仓库或者远程仓库没有该分支，用该命令创建远程仓库分支。

`git push <远程仓库本地别名> --delete <远程仓库分支名>`：删除远程仓库分支。



## 14.从远程库克隆

`git clone git@github.com:RawOnion/gitskills.git`：`SSH`协议版本。

`git clone https://github.com/RawOnion/gitskills.git`：`https`协议版本



## 15.查看远程库信息

`git remote -v`



## 16.抓取远程仓库新提交

`git pull`



## 17. 创建本地分支和远程分支的链接关系

`git branch --set-upstream-to <branch-name> <远程仓库本地别名(origin)>/<branch-name>`



## 18.查看分支

`git branch`



## 19.创建分支

`git branch <name>`



## 20.切换分支

`git checkout <name>`或者`git switch <name>`



## 21.创建+切换分支

`git checkout -b <name>`或者`git switch -c <name>`



## 22.合并某分支到当前分支

`git merge <name>`



## 23.删除分支

`git branch -d <name>`



## 24.创建标签

`git tag <name>`：默认当前分支的`HEAD`提交节点



## 25.查看标签

`git tag`：查看所有标签(按字母排序)



## 26.查看标签信息

`git show <tagname>`



## 27.推送本地标签到远程仓库

`git push origin <tagname>`：推送一个本地标签；

`git push origin --tags`：推送全部未推送过的本地标签；



## 28.删除本地标签和远程标签

`git tag -d <tagname>`：删除一个本地标签；

`git push origin :refs/tags/<tagname>`：删除一个远程标签。



## 29.配置别名

`git config --global alias.st status`：全局状态下为命令`status`配置别名，`git status`可以用`git st`来替换