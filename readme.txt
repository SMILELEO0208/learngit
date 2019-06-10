Git is a distributed version control system.
Git is free software.

Git has a mutable index called stage.

常用命令：
git init : 初始化一个Git仓库
git add filename : 提交文件到暂存区
git status : 查看仓库的当前状态(是否被修改)
git diff filename : 查看修改的内容
git commit : 提交文件到仓库
git log : 查看最近到远的提交日志
git reset : 回退版本，例如：
		    git reset --hard HEAD^ ：回退到上一个版本
		    git reset --hard HEAD^ ：回退到上上一个版本
		    git reset --hard HEAD~n : 回退到第n个版本，n是正整数
		    git reset --hard tempid ：tempid 是想回退到的那个版本的commit id的前几位
git reflog ： 查看命令历史记录(主要是commit 和 reset 命令的记录)
git checkout --filename : 撤销对工作区的修改；这个命令是以最新的存储时间节点（add和commit）为参照，覆盖工作区对应文件file；这个命令改变的是工作区
git checkout filename : 切换到另一个分支
git reset HEAD --filename : 清空add命令向暂存区提交的关于file文件的修改(Ustage);这个命令仅改变暂存区，不改变工作区，这意味着在无任何其他操作的情况下，工作区中的实际文件同该命令运行之前无任何改变
git rm filename : 从版本库中删除文件，并且需要git commit才有效

先有本地库，后有远程库，两者关联命令：
git remote add origin https://github.com/Github账号/learngit.git----关联远程库命令
  或者是 git remote add origin git@github.com:Github账号/learngit.git
git push -u origin master


现有远程库，从远程库克隆一个本地库的命令：
git clone git@github.com:Github账号/gitskills.git

git checkout -b dev：创建分支dev
git branch：查看分支
git merge dev：合并分支
git branch -d dev：删除分支

git log --graph：查看分支合并图
git merge --no-ff -m "remark" <name> : 普通合并模式，禁用fast forward,同时创建了一个commit提交

git stash: 保存当前的工作现场
git stash list ：查看stash 信息
git stash apply: 恢复stash，但是并没有删除stash
git stash drop：删除恢复的stash
git stash pop: 恢复的同时把stash内容也删，等同于上面两个命令（apply 和 drop）
git stash apply stash@{n}：恢复指定的stash，n正整数，表示第n个stash
stash的apply、 drop、pop 都可以加上stash@{n}，对指定的stash进行操作



名词解释：
工作区：本地电脑上能看到的目录
版本库：工作区内隐藏的.git文件夹,就是Git的版本库。
暂存区：版本库中最重要的就是称为stage(或者index)的暂存区。
版本库里还有Git为我们自动创建的第一个分支master，以及指向master的指针HEAD。
远程仓库：是指托管在网络上的项目仓库。
GitHub：就是提供git仓库托管服务的神奇网站。
本地git仓库和GitHub上的git仓库之间的传输是通过SSH加密的，所以需要设置SSH key。
SSH创建：本地根目录下是否有.ssh文件，如果存在查看是否有id_rsa和id_rsa.pub这两个文件，如果没有，可以使用如下命令创建SSH,
		$ ssh-keygen -t rsa -C"youremail@example.com" ，输入该命令后的操作都可以直接按回车键默认配置。
GitHub 配置SSH Keys，是为了识别出你推送的提交确实是你推送的，非别人冒充的。

抓取分支：现在多了一个小伙伴一起工作，想从master的dev分支上开发工作，必须得先把dev分支push到远程库，新的伙伴再从远程库dev上获取。
		 git push origin dev
		 git branch dev origin/dev
多人协作：1.抓取分支
		2.开发，推送自己的修改
		3.如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
		4.如果合并有冲突，则解决冲突，并在本地提交；
		5.没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。


Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。


Creating a new branch is quick and simple.

禁用fast forward模式

merge with no-ff 

rebase test