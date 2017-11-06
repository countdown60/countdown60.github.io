
git 常用操作命令

`git init`:把当前目录初始化成git仓库

把文件添加到仓库步骤:
   1. `git add <file>`命令:  把文件添加到仓库,实际上是把文件修改添加到暂存区

   2. `git commit`命令: 把文件提交到仓库,实际上是把暂存区的所有内容提交到当前分支. 注意,该命令后面一般加 -m 参数,来写提交说明; 该命令可以一次提交多份文件到仓库

 `git status`: 查看仓库当前状态

 `git diff <file>` : 查看文件变更

 `git log `: 查看提交历史,可以在后面带上文件名,查看单一文件的变更记录


 在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

`git reset `: 回退到某个版本; 参数 --hard

`git reflog`: 记录每一次命令,可以用来版本回退.

![工作区和版本库](http://www.liaoxuefeng.com/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

git中为什么需要暂存区?有时候需要临时保存,但是又不想提交到分支,可以放到暂存区

**撤销修改:**
` git checkout -- <file>`: 把该文件在工作区内的修改全部撤销,即把文件恢复到最近一次add或者commit的状态.如果add但是没有commit的话,可以使用git reset来撤销暂存区修改.

>场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

>场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

**删除文件**: `git rm <file>`命名删除文件后,'git commit'提交,即完成


#### 关联远程库

把本机的ssh公钥添加到github的sshkey中(非必选)

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git；`

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

git支持多种协议,如https和ssh,https速度较慢且需要输入口令,而ssh(git://使用ssh)需要添加公钥到远程仓库,但速度快.

克隆远程库: `git clone`,克隆的事master分支,如果要dev分支的话,需要`git checkout -b dev origin/dev`来创建远程的dev在本地的分支.

### 分支管理

创建分支:  `git branch <branch-name>`

切换分支: `git checkout <branch-name>`

或者:

创建并切换分支: `git checkout -b <branch-name>`

分支合并: `git merge <branch-name>`,把指定分支的内容合并到当前分支,命令`git branch`可以查看当前分支.

分支合并有普通模式和'fast forward'模式,区别在于有没有合并历史.

删除分支: `git branch -d <branch-name>`

因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。

用`git log --graph`命令可以看到分支合并图。

#### 分支策略

master分支非常稳定,通常用于发布新版本;dev 分支常用于开发过程,且每个人都有自己的分支,往dev分支进行合并.

**bug分支**

每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它.

当你需要紧急修复某个bug,而当前dev分支还未合并,可以使用`git stash`命令,把当前工作现场“储藏”起来，等以后恢复现场后继续工作.

修复bug时,首先要确认去哪个分支修复bug,在哪个分支上修复,就在该分支上创建bug分支.

修复完成并合并分支后,删掉bug分支,然后用回到dev分支继续做之前的事.此时,可以用'git stash list'来查看之前保留的工作内容,然后用`git stash pop`来恢复工作内容.

**Feature分支**
开发一些新功能或者实验性质代码的时候,需要创建Feature分支,防止弄乱分支.

查看远程库信息:  `git remote -v`


#### 多人协作
多人协作的工作模式通常是这样：

首先，可以试图用git push origin branch-name推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。


### 标签管理

发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。


为什么要有标签? 因为如果用commit确定版本的话,由于commit事一串无规律的字符串,不容易书写和记忆.而tag是一个容易记住的有意义的名字,tag和某个commit绑定.

**创建标签**: `git tag -a <tag-name> -m "XXX"`,可以加上参数-a指定标签名,-m指定说明文字,-s 用私钥签名一个标签(需要安装gpg)

**查看所有标签** : `git tag`

**删除标签**: `git tag -d <tag-name>`(未推送时删本地,远程另外的方法 )

**推送标签** : `git push origin　<tag-name>`

### 自定义git

忽略某些文件时，需要编写.gitignore；

.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！


 **别名** : 可以用git config来配置git命令的别名!!!
