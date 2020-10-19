## 101

### Git Account Config
```
git config --global user.email "theEmail@example.com"
git config --global user.name "theNickname"
```
Example: AndrewEmail, kaleido97

### Get or Create Files for the Project
```
cd whereYouWantToCreateThisProject
git init
git clone urlOfRemoteRepo
```

todo: 将remote add提前于clone，并用pull替代clone <br/>
Maybe:
``` 
git remote add origin urlOfRemoteRepo    # 将本地关联至远程repository，并将远程repo简称为origin
git pull origin branchRemote:branchLocal # 从origin的branchRemote分支中拉取内容至本地branchLocal分支
```

### Connect Local & Remote Repos
```
git remote add origin urlOfRemoteRepo    # 将本地关联至远程repository，并将远程repo简称为origin
git remote 
git remote -v
git remote show origin
```

### Connect Branches
```
git checkout -b / switch -c newBranchLocal      # 在本地创建并切换至新分支
(Same as: git branch newBranchLocal + git checkout/switch newBranchLocal)
(git checkout branchLocal origin/branchRemote   # 如果远程有某一个分支而本地没有，该命令将远程的分支迁到本地)
git branch / branch -r / branch -a		        # 查看本地/远程/所有分支

git branch --set-upstream-to=origin/branchRemote branchLocal	# 关联本地及远程分支
```

### Edit Files, Commit to Local Repo, and Push to Remote Repo 
```
<edit those files>
git status			                            # 查看当前文件状态（是否add、commit等）
git add *
git commit -m "Changes for files"
git push                                    # 适用于之前关联过本地与远程分支后

(Otherwise:)
git push -u origin branchRemote
# 由于远程库是空的，我们第一次推送branchLocal分支时，加上了-u参数，
# Git不但会把本地的branchLocal分支内容推送到远程的新的branchRemote分支，
# 还会把本地的branchLocal分支和远程的branchRemote分支关联起来，
# 在以后的推送或者拉取时就可以简化命令

git push --set-upstream origin branchRemote # 若之前push时未加-u，则可之后再通过--set-upstream来关联本地及远程
```
