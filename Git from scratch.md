## ���������ʽ

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

����clone��ɸ�Ϊ��
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
�����֮ǰ��δcommit�����򿴲���branch��Ϣ��

git branch --set-upstream-to=origin/branchRemote branchLocal	# �������ؼ�Զ�̷�֧
```

### Edit Files, Commit to Local Repo, and Push to Remote Repo 
```
<edit those files>
git status                          # �鿴��ǰ�ļ�״̬���Ƿ�add��commit�ȣ�
git add *
git commit -m "Changes for files"   
git push                            # ������֮ǰ������������Զ�̷�֧��

(Otherwise:)
git push -u origin branchRemote
---------------
git push origin localBranchName:remoteBranchName
---------------
# ����Զ�̿��ǿյģ����ǵ�һ������branchLocal��֧ʱ��������-u������
# Git������ѱ��ص�branchLocal��֧�������͵�Զ�̵��µ�branchRemote��֧��
# ����ѱ��ص�branchLocal��֧��Զ�̵�branchRemote��֧����������
# ���Ժ�����ͻ�����ȡʱ�Ϳ��Լ����

git push --set-upstream origin branchRemote # ��֮ǰpushʱδ��-u�����֮����ͨ��--set-upstream���������ؼ�Զ��
```

push����ܻ���ֳ�ͻ��terminal��ʾ��Ҫ��pull�� <br/>
pull֮ǰ����stash��ʱ�洢�����޸ģ���pull֮����unstash��
```
git stash save -a "stashName"
git pull
git stash apply
```

����stash��
```
Ref: https://www.cnblogs.com/tocy/p/git-stash-reference.html
git stash save -a "stashName"   # ����stash��-a��ʾstash��ǰĿ¼�µ������޸ģ�����untracked files��ignored files
git stash list                  # �鿴��ǰ������stash
git stash show <stashName>      # �鿴ָ��stash�ж��ļ����ĵ����
git stash show <stashName> -p   # �鿴ָ��stash�ж��ļ����ĵ���ϸ���

git stash pop <stashName>       # Ӧ��stash��ɾ��
git stash apply <stashName>     # Ӧ��stash����ɾ��
git stash drop <stashName>      # ɾ����ΪstashName��stash

git stash branch newBranch      # ����һ���µķ�֧�����ⲿ��stash��ԭ��֧��stash����ɾ��
```

������ͨ��stash������ֱ���޸ĳ�ͻ�� <br/>
��ͻ�Ĳ鿴�ж��ְ취��������ʹ��```git diff```����ԭ�ļ����Ҳ���Ȼ���޸ģ�
������webstorm��������Ҽ�����ļ�commit directory��Ȼ����ĳ���ļ��鿴�Ķ��ĵط���
���⻹����ʹ��Beyond Compare���ⲿ��������޸ġ�


## �ֶ�����zip�ļ�����ʽ

���ǵ������ص�zip�ļ���������clone����δ��Զ�����ӹ�����ӦΪ��

### Init
```
cd locationOfZipFile                            # ��ʼ��Git֮ǰȷ����Ŀ·��
git init                                        # ��ʼ��Git���������زֿ�
git checkout -b / switch -c newBranchLocal      # �ڱ��ش������л����·�֧
```
֮�����```git status, git log```����ʱ���е��ԡ�

### Connect to Remote Repo
```
git add *                                       # �����ļ��ı༭�ύ���ݴ�����*��ʾȫ���ļ�
git commit -m "msg"                             # ���ݴ������޸��ύ�����زֿ⣬ִ�к�Ż��������ɱ��ط�֧

git remote add origin theURL    # �����زֿ������Զ�ֿ̲⣬����Զ�ֿ̲��Ϊorigin
                                # �ڵ�һ��commit֮ǰ��Ĭ�ϵ�ǰbranchδ����������git remote add����Ч��
```

���remote��������µ��ԣ�
```
git remote
git remote -v
git remote show origin
```
commit���֧����������������```git branch / branch -r/ branch -a```�Ƚ��е��ԡ�

### Pull & Push
����Զ�ֿ̲�󣬿�ʼ��Զ�ֿ̲�push�ύ�޸ġ�push֮ǰ��Ҫ��pull��
```
git stash save -a "stashName"   # ����Ӧ��pull֮ǰstash���θ��ģ�pull֮����unstash��Ȼ��push
                                # ���ڱ���ֱ��������zipԴ�ļ���û��������ǰ��Զ�̹����������ⲽ����

git pull origin remoteBranch --allow-unrelated-histories    # ��Զ��origin�ֿ��е�remoteBranch��֧������pull����
                                                            # ����֮ǰδ��Զ�̹���������Ҫallow unrelated Git history               
```
pull֮����ܻᱨ����ʾ��Щ�ļ���Ҫmerge�� <br/>
���ڱ���ֱ��������zipԴ�ļ���û��������ǰ��Զ�̹��������޷�ʹ��������stash��ֻ���ֶ��޸ġ�

��ʱ����Ҫ����git diff��ʹ����Beyond Compare�������Щ�ļ������ֶ��޸ġ� <br/>
����git diff�����ո���ʾ�������ݣ���q�˳���ǰdiffģʽ����ԭ�����ļ��С�>>>>����Ĳ��ֽ����޸ġ�

�ĵ�û�г�ͻΪֹ����push��
```
git push origin localBranch:remoteBranch    # �����ص�localBranch��֧���������͵�Զ��origin�ֿ��remoteBranch��֧��
```
