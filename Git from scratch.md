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

todo: ��remote add��ǰ��clone������pull���clone
Maybe:
``` 
git remote add origin urlOfRemoteRepo    # �����ع�����Զ��repository������Զ��repo���Ϊorigin
git pull origin branchRemote:branchLocal # ��origin��branchRemote��֧����ȡ����������branchLocal��֧
```

### Connect Local & Remote Repos
```
git remote add origin urlOfRemoteRepo    # �����ع�����Զ��repository������Զ��repo���Ϊorigin
git remote 
git remote -v
git remote show origin
```

### Connect Branches
```
git checkout -b / switch -c newBranchLocal      # �ڱ��ش������л����·�֧
(Same as: git branch newBranchLocal + git checkout/switch newBranchLocal)
(git checkout branchLocal origin/branchRemote   # ���Զ����ĳһ����֧������û�У������Զ�̵ķ�֧Ǩ������)
git branch / branch -r / branch -a		        # �鿴����/Զ��/���з�֧

git branch --set-upstream-to=origin/branchRemote branchLocal	# �������ؼ�Զ�̷�֧
```

### Edit Files, Commit to Local Repo, and Push to Remote Repo 
```
<edit those files>
git status			                        # �鿴��ǰ�ļ�״̬���Ƿ�add��commit�ȣ�
git add *
git commit -m "Changes for files"
git push                                    # ������֮ǰ������������Զ�̷�֧��

(Otherwise:)
git push -u origin branchRemote
# ����Զ�̿��ǿյģ����ǵ�һ������branchLocal��֧ʱ��������-u������
# Git������ѱ��ص�branchLocal��֧�������͵�Զ�̵��µ�branchRemote��֧��
# ����ѱ��ص�branchLocal��֧��Զ�̵�branchRemote��֧����������
# ���Ժ�����ͻ�����ȡʱ�Ϳ��Լ�����

git push --set-upstream origin branchRemote # ��֮ǰpushʱδ��-u�����֮����ͨ��--set-upstream���������ؼ�Զ��
```
