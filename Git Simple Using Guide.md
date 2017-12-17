# Git 初步使用方法
## 一： 安装Git：
### WIN安装：  
> 下载GIT：[下载连接](https://git-scm.com/download/win)  
执行EXE文件进行安装。
### Ubuntu安装：  
> apt-get update  
apt-get install git  


## 二： 初始配置
### 2.1 配置本地Git账号的Name，Email：
#### 在桌面右键单击“Git Bash Here”，输入如下命令：  
> $ git config --global user.name "用户名"  
$ git config --global user.email "邮箱"  

### 2.2 检查是否配置成功：
#### 在Git Bash中输入：  
> $ git config --list
#### 会有如下打印：
> user.name=jaya  
user.email=qq416296378@Jaya

## 三： 简单使用
### 3.1 初始化Git仓库
1. 打开一个工程文件夹（例如：\Git操作流程\test_git）
2. 右键单击“Git Bash Here”，打开Git Shell。
3. 输入git init 进行初始化Git仓库：
> $ git init  
Initialized empty Git repository in C:/Users/qq416/Desktop/Git操作流程/test_git/.git/
4. 初始化完成后，在工程目录下会出现一个“.git”的隐藏文件夹。
> $ ls -a  
./  ../  .git/  hello.py  Readme.md

### 3.2 使用Git管理本地代码：
#### 在开始使用前，需要了解三个概念： 
>HEAD：用户空间，即用户修改代码存储的位置。  
Index：暂存区域，引用的指针，会指向最新提交的快照。  
Working Directory：仓库，历史提交都在这里。
#### 开始使用：(以“\Git操作流程\test_git”为例)
#### 查看当前状态：
> $ git status  
On branch master  
Initial commit  
Untracked files:  
  (use "git add <file>..." to include in what will be committed)  
        Readme.md  
        hello.py  
nothing added to commit but untracked files present (use "git add" to track)  

PS：使用“git status ”查看当前工作空间状态  
通过反馈的信息，可以了解到两个文件“Readme.md”“hello.py”并没有被Git跟踪。

#### 将要追踪的文件添加进暂存区域：  
> $ git add Readme.md  
$ git add hello.py  
$ git status  
On branch master
Initial commit  
Changes to be committed:  
  (use "git rm --cached <file>..." to unstage)  
        new file:   Readme.md  
        new file:   hello.py  

PS：使用“git add *** ”命令会将***文件加入暂存区域进行跟踪。  
如果要加入目录全部文件也可以用“git add * ”指令。

        
#### 将暂存区域的文件保存在仓库中：
> $ git commit -m "Old Version!"  
[master (root-commit) 87aba18] Old Version  
 2 files changed, 2 insertions(+)  
 create mode 100644 Readme.md  
 create mode 100644 hello.py  

$ git log  
commit 87aba18674d701755bcc871daf1fbc14318c1142  
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:05:42 2017 +0800  
    Old Version  

PS：“git commit -m "Old Version!"”将暂存区域的文件保存在仓库，-m参数是备注的意思。  
“git log”可以查看当前目录下的Git版本的使用情况。  
    
#### 随意修改“Readme.md”后再存入仓库一个版本：
> $ git status  
On branch master  
Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git checkout -- <file>..." to discard changes in working directory)  
        modified:   Readme.md  
no changes added to commit (use "git add" and/or "git commit -a")  

PS:我们发现修改后的文件和暂存区域的文件不一致，所以需要将修改后的文件添加至暂存区域。  

$ git add Readme.md  
$ git status  
On branch master  
Changes to be committed:  
  (use "git reset HEAD <file>..." to unstage)  
        modified:   Readme.md  

$ git commit -m "back to history test"  
[master 50304f9] back to history test  
 1 file changed, 1 insertion(+)  

$ git log  
commit 50304f9041438f61a7a88c0ceb29ee4b34b669e3  
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:17:55 2017 +0800  
    back to history test  
commit 87aba18674d701755bcc871daf1fbc14318c1142  
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:05:42 2017 +0800  
    Old Version  

#### 回到Old Version版本通过commit
> $ git log  
commit 50304f9041438f61a7a88c0ceb29ee4b34b669e3  
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:17:55 2017 +0800  
    back to history test  
commit 87aba18674d701755bcc871daf1fbc14318c1142   
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:05:42 2017 +0800  
    Old Version  

$ git checkout 87aba1  
Previous HEAD position was 50304f9... back to history test  
HEAD is now at 87aba18... Old Version  

PS：这样我们已经回到Old Version版本了。commit号码只需要输入前几位就可以。  

$ git log  
commit 87aba18674d701755bcc871daf1fbc14318c1142  
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:05:42 2017 +0800  
    Old Version  

PS：可以看见log中的最新版本已经不见，不过他并没有丢失，我们可以通过--all参数找到。  

$ git log --all  
commit 50304f9041438f61a7a88c0ceb29ee4b34b669e3  
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:17:55 2017 +0800  
    back to history test  
commit 87aba18674d701755bcc871daf1fbc14318c1142  
Author: jaya <qq416296378@Jaya>  
Date:   Sat Dec 16 17:05:42 2017 +0800  
    Old Version  

### 3.3 使用Git分支功能：
#### 了解分支概念： 
> 分支是非常有用的功能，Git会自动为我们创建一个master分支，之前的操作都是在master分支上直接操作，很多情况下都会不方便，比如：多人协作，并行修改多个bug，有多个版本需求。所以出现了分支的概念。  
用户只需要创建新的分支，在新的分支上做出修改，同时不会影响到master分支。  
用户在新的分支上完成功能，可以将新的功能合并进master分支。  
用可以随意的在分支间进行切换。

#### 查看分支：
> $ git branch  
\* (HEAD detached at 87aba18)  
  master  

PS：可以发现目前我们只有一个master分支。HEAD为当前指针。

#### 创建分支：
> $ git checkout -b test_branch  
Switched to a new branch 'test_branch'  

$ git branch  
  master  
\* test_branch  

PS:
使用“git checkout -b test_branch ”添加分支后自动跳转到新的分支。  
也可以使用“git branch *** ”来创建分支。（不会跳转到新的分支）  
使用“git checkout *** ”跳转到新的分支。

#### 修改新分支后存入仓库：
> $ git log --decorate --oneline --graph --all  
\* 50304f9 (HEAD -> test_branch, master) back to history test  
\* 87aba18 Old Version  

$ git status  
On branch test_branch  
Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git checkout -- <file>..." to discard changes in working directory)  
        modified:   Readme.md  
no changes added to commit (use "git add" and/or "git commit -a")  

$ git add \*  

$ git commit -m "test branch!"  
[test_branch 2c4decf] test branch!  
 1 file changed, 2 insertions(+), 1 deletion(-)  

$ git log --decorate --oneline --graph --all  
\* 2c4decf (HEAD -> test_branch) test branch!  
\* 50304f9 (master) back to history test  
\* 87aba18 Old Version  

PS：可以看见更新仓库后，目前HEAD指针指向test_branch所在的“2c4decf”分支。  
“git log --decorate --oneline --graph --all”说明如下：  
--decorate 显示所有引用  
--oneline 精简显示  
--graph 图形化显示  
--all 显示全部

#### 合并分支：
> $ git checkout master  
Switched to branch 'master'  

$ git log --decorate --oneline --graph --all  
\* 2c4decf (test_branch) test branch!  
\* 50304f9 (HEAD -> master) back to history test  
\* 87aba18 Old Version  

$ git merge test_branch  
Updating 50304f9..2c4decf  
Fast-forward  
 Readme.md | 3 ++-  
 1 file changed, 2 insertions(+), 1 deletion(-)  

$ git log --decorate --oneline --graph --all  
\* 2c4decf (HEAD -> master, test_branch) test branch!  
\* 50304f9 back to history test  
\* 87aba18 Old Version  

$ git branch -d test_branch  
Deleted branch test_branch (was 2c4decf).  

$ git log --decorate --oneline --graph --all  
\* 2c4decf (HEAD -> master) test branch!  
\* 50304f9 back to history test  
\* 87aba18 Old Version  

PS：首先切换到master分支上。  
使用“git merge test_branch ”命令将“test_branch”分支合并到master上。  
使用“git branch -d test_branch ”删除test_branch。（当然也可以不删除）  
并不是每次操作都必须要使用“git log --decorate --oneline --graph --all”命令，输入“git log --decorate --oneline --graph --all”命令指示为了更容易观察Git的版本控制过程
