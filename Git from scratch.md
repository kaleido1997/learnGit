## 纯代码的形式

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

这里clone或可改为：
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
（如果之前从未commit过，则看不到branch信息）

git branch --set-upstream-to=origin/branchRemote branchLocal	# 关联本地及远程分支
```

### Edit Files, Commit to Local Repo, and Push to Remote Repo 
```
<edit those files>
git status                          # 查看当前文件状态（是否add、commit等）
git add *
git commit -m "Changes for files"   
git push                            # 适用于之前关联过本地与远程分支后

(Otherwise:)
git push -u origin branchRemote
---------------
git push origin localBranchName:remoteBranchName
---------------
# 由于远程库是空的，我们第一次推送branchLocal分支时，加上了-u参数，
# Git不但会把本地的branchLocal分支内容推送到远程的新的branchRemote分支，
# 还会把本地的branchLocal分支和远程的branchRemote分支关联起来，
# 在以后的推送或者拉取时就可以简化命令。

git push --set-upstream origin branchRemote # 若之前push时未加-u，则可之后再通过--set-upstream来关联本地及远程
```

push后可能会出现冲突，terminal提示需要先pull。 <br/>
pull之前可以stash暂时存储本地修改，在pull之后再unstash：
```
git stash save -a "stashName"
git pull
git stash apply
```

关于stash：
```
Ref: https://www.cnblogs.com/tocy/p/git-stash-reference.html
git stash save -a "stashName"   # 创建stash，-a表示stash当前目录下的所有修改，包括untracked files和ignored files
git stash list                  # 查看当前的所有stash
git stash show <stashName>      # 查看指定stash中对文件更改的情况
git stash show <stashName> -p   # 查看指定stash中对文件更改的详细情况

git stash pop <stashName>       # 应用stash并删除
git stash apply <stashName>     # 应用stash但不删除
git stash drop <stashName>      # 删除名为stashName的stash

git stash branch newBranch      # 创建一个新的分支保存这部分stash，原分支的stash将被删除
```

若不想通过stash，而是直接修改冲突： <br/>
冲突的查看有多种办法，首先是使用```git diff```，在原文件中找差异然后修改；
或者在webstorm中用鼠标右键点击文件commit directory，然后点击某个文件查看改动的地方；
另外还可以使用Beyond Compare等外部程序进行修改。


## 手动下载zip文件的形式

若是单独下载的zip文件（即不需clone），未与远程连接过，则应为：

### Init
```
cd locationOfZipFile                            # 初始化Git之前确认项目路径
git init                                        # 初始化Git，创建本地仓库
git checkout -b / switch -c newBranchLocal      # 在本地创建并切换至新分支
```
之后可用```git status, git log```等随时进行调试。

### Connect to Remote Repo
```
git add *                                       # 将对文件的编辑提交至暂存区，*表示全部文件
git commit -m "msg"                             # 将暂存区的修改提交至本地仓库，执行后才会真正生成本地分支

git remote add origin theURL    # 将本地仓库关联至远程仓库，并将远程仓库称为origin
                                # 在第一次commit之前，默认当前branch未创建，所以git remote add是无效的
```

添加remote后可用如下调试：
```
git remote
git remote -v
git remote show origin
```
commit后分支才真正建立，可用```git branch / branch -r/ branch -a```等进行调试。

### Pull & Push
连接远程仓库后，开始向远程仓库push提交修改。push之前需要先pull：
```
git stash save -a "stashName"   # 正常应在pull之前stash本次更改，pull之后再unstash，然后push
                                # 由于本次直接下载了zip源文件，没有在下载前与远程关联，所以这步跳过

git pull origin remoteBranch --allow-unrelated-histories    # 将远程origin仓库中的remoteBranch分支的内容pull下来
                                                            # 由于之前未与远程关联，故需要allow unrelated Git history               
```
pull之后可能会报错，提示有些文件需要merge。 <br/>
由于本次直接下载了zip源文件，没有在下载前与远程关联，故无法使用上述的stash，只能手动修改。

这时则需要输入git diff或使用如Beyond Compare软件对这些文件进行手动修改。 <br/>
输入git diff，摁空格显示更多内容，摁q退出当前diff模式，在原程序文件中”>>>>“间的部分进行修改。

改到没有冲突为止，再push：
```
git push origin localBranch:remoteBranch    # 将本地的localBranch分支的内容推送到远程origin仓库的remoteBranch分支中
```
