title: Git入门
date: 2015/11/18
categories: 教程
tags: Git
toc: true
---


### 在Windows上安装
msysgit是windows版的git，下载地址：[msysgit](https://git-for-windows.github.io/)，然后选择默认安装即可。开始菜单找到Git->Git Bash，打开弹出类似命令行的窗口就安装成功了，安装完成后在命令行输入：
```bash
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```
注意：`git config`命令的`--config`参数说明这台机器上所有的Git仓库都会使用这个配置，也可以对某个仓库指定不同的用户名和Email


<!--more-->

### 创建版本库
版本库就是一个仓库REPOSITORY，也可以理解成就是一个目录，这个目录里面所有的文件都可以被Git管理起来，每个文件的修改删除Git都能跟踪和还原

创建一个版本库很简单，选择一个合适的目录（目录不要包含中文，否则可能会出现莫名其妙的错误），右键选择GIt Bush Here弹出命令行窗口，输入
```bash
git init
```
命令行返回`Initialized empty Git repository in /xx/xx/xx/.git/`则说明仓库已经建好，而且高速你这是一个空仓库，目录中出现一个.git目录，如果你没看到可能它隐藏了，并且不能删掉这个目录也不能乱改

在目录下新建一个readme.txt（推荐使用Sublime-Text3，不要使用windows的记事本因为它会在每个文件开头添加了0xefbbbf（十六进制）的字符，会遇到很多不可思议的问题），内容如下
```
Git is a version control system.
Git is free software.
```
然后把文件放到Git仓库只需二步，第一步把文件添加到仓库
```bash
git add readme.txt
```
第二步把文件提交到仓库
```bash
git commit -m "wrote a readme.txt file"
```
注意：-m参数是提交时的参数说明，不能省略否则会报错，平时使用时可以多次git add添加文件然后一次git commit提交所有已经添加的文件

### 版本管理
#### 1.版本库状态
在之前创建的文件的目录里输入如下命令可以查看当前仓库的状态，主要仓库状态有修改未添加未提交，修改已添加未提交，修改已添加已提交等
```bash
git status
```

如果你修改文件后输入如下命令来查看具体修改了哪些内容,知道修改了哪些内容后再执行`git add`和`git commit`就放心多了，期间也可以用`git status`随时查看仓库的状态
```bash
git diff readme.txt
```
#### 2.版本回退
当我们提交了2次更改后发现需要回退到之前的版本，可以先输入如下的命令查看之前提交的历史记录`git log`命令显示最近到最远的提交日志
```bash
git log
```
命令行窗口返回如下内容（举例）
```
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file
```
注意：`git log`命令显示最近到最远的提交日志，每一行前面的一串字符串是commit id之后用来作为回退的标记，后面的“append GPL”是当时提交的描述说明（到此可见当时加上描述还是满需要的，否则分不清提交了什么），每提交一次`git log`就会多一条记录

现在开始回退到上一版本，命令如下
```bash
git reset --hard HEAD^
```
注意:HEAD表示当前版本，HEAD^表示上一版本（也可以用具体的commit id代替HEAD^），以此类推，--hard代表的意思可以先不管，然后打开readme.txt文件查看是不是会退了上一版本，如果你回退多次（或者重启过电脑）后已经不知道commit id了，那么还是有办法的，输入如下命令可以查看命令历史（之前的git log是提交历史）
```bash
git reflog
```
返回如下数据到窗口
```
ea34578 HEAD@{0}: reset: moving to HEAD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file
```
之前每次提交的commit id又都出现了，又可以愉快的回退到各版本了

#### 3.管理修改
这一节需要注意的是你commit的文件前提是已添加（就是执行过git add），如果没有添加则不会commit到仓库，如果还要commit到仓库则还需要执行一边git add
#### 4.撤销修改
如果你添加了文件但是没有提交，发现里面有不合适的内容如何破，执行如下命令，让文件回到最近一次git commit或git add时的状态
```bash
git checkout -- readme.txt
```
注意：还可以使用`git reset HEAD file`以把暂存区的修改撤销掉，`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区(git add后)

#### 5.删除文件
一种就是你未提交的文件可以直接在文件管理器中删除，然后`git status`知道你删除了文件，再执行`git commit`就可以了

还有一种可能就是你提交了文件，可以执行`git rm`并且`git commit`就可以了，这种情况不用担心误删，你还可以用之前学到的命令恢复

### 远程仓库
到目前为止你的你所操作的文件都是在你本地的机器上，如果硬盘挂了那就麻烦了，接下来把你的本地仓库托管到GitHub上
#### 1.添加远程仓库
由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以第一步要创建SSH Key，在命令行窗口执行以下命令
```bash
ssh-keygen -t rsa -C "youremail@example.com"
```
可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人

第二步登陆GitHub（事先注册好GitHub帐号），打开“Account settings”，“SSH Keys”页面，然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，如果你又多台电脑可以重复这一步添加SSH Key

第三步登入GitHub创建一个仓库learn-git,然后在本地的learn-git目录输入如下命令
```bash
git remote add origin git@github.com:yourusername/learngit.git
```
然后把你本地的仓库推送到GitHub
```bash
git push -u origin master
```
第一次推送要加-u参数，次操作会把本地的master分支和远程的master分支关联起来，推送成功后可以登入网页端查看推送的内容和本地一致，以后只要修改了内容就可以执行`git push -u origin master`推送到GitHub
#### 2.从远程仓库克隆
之前说的是先有本地库然后关联远程库，现在看现有远程库然后本地克隆远程的，在GitHub新建一个仓库git-skills，此时远程的仓库已经准备好，现在在本地执行如下命令
```bash
git clone git@github.com:yourusername/git-skills.git
```
如果多人开发，每个人都可以从这个仓库克隆到本地

[廖雪峰的Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)写下来的，算是读书笔记吗？
链接：http://www.liaoxuefeng.com/，如有问题，请联系我删除此文章