# Git notes

## 基本
### 设置用户名、邮箱
> git config --global user.name "kwdhd"
> git config --glbbal user.email "kwdhdts@gmail.com"


### 初始化一个新仓库
> git init 

### 把文件添加到 Git
文件修改了也要通过add添加之后才能commit
> git add filename

### 文件提交到仓库
> git commit -m "remark"

### 查看文件状态
> git status

### 查看文件修改内容
> git diff filename 

### 查看提交日志
> git log

查看指定文件的日志
> git log filename

显示在一行
> git log --pretty=oneline

图形化展示
> git log --graph

美化展示
>git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"


### 版本回退
> git reset --hard HEAD~100 or commit id

### 查看历史命令
> git reflog

## 暂存区
工作区 -> 暂存区 -> 版本

### 丢弃工作区的修改
> git checkout -- filename 

### 丢弃暂存区的修改
> git reset HEAD filename


### 删除文件
> rm filename
> git rm filename
> git commit -m 'remark'

### 恢复删除
删除文件未提交时
> git checkout -- filename


## Github

### 创建密匙
密匙文件生成在 ~/.ssh文件夹中，id_rsa 是私匙，id_rsa.pub 是公匙添加到Github的 SSH Key中
> ssh-keygen -t rsa -C "kwdhdts@gmail.com"

### 创建远程仓库
在Github上找到 `create a new repo`  按钮，输入仓库名即可创建一个新仓库。


### 关联远程仓库
> git remote add origin git@github.com:用户名/仓库名.git

### 将本地仓库内容推送到远程仓库
> git push -u  origin master

### 克隆远程库
> git clone git@github.com:用户名/仓库名.git


## 分支管理

### 新建分支
创建分支并切换
> git checkout -b wor
等于
> git branch name
> git checkout name


### 合并分支
> git merge 分支名

### 删除分支
> git branch -d 分支名

### 暂存分支
可以将分支内容暂存起来，不用提交
> git stash

查看暂存区
> git stash list

恢复暂存区
> git stash apply

恢复暂存区同时删除暂存区
> git stash pop