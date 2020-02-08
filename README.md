#### 常用命令
==1、查看状态==

`git status`

> 查看工作区和暂存去状态

==2、添加到暂存区==

`git add [file name]`

> 将工作区“新建/修改”添加到暂存区，“修改”可以跳过这一步

==3、提交到本地版本库==

`git commit -m "commit message" [file name]`

> `-m "commit message"`可以不写，但需要在下一步在vim里面填写，所以最好加上

==4、查看历史记录==

`git log` //完整的内容，多屏内容：空格翻页，b上翻页，q退出

`git log --pretty=oneline` //一条记录显示一行,hash值完整

`git log --oneline`//一条记录显示一行,hash值部分

`git reflog` //一行，简hash，则仍增历史版本位置：`HEAD@{0}`

==5、版本前进后退==
1. git reset --hard[简版hash]  //推荐
2. git reset --hard HEAD^  //只能后退，一个^代表后退一步
3. git reset --hard HEAD~n  //只能后退，n代表后退n步

#### 安装Git

官网下载默认安装即可：https://git-scm.com/

#### 提交代码

工作去 -> 暂存区 -> 版本库

代码提交流程：

本地库--(`git init`)-->初始化仓库--(`git add`)-->暂存区/索引--(`git commit`)-->版本库(github等)

Windows下，进入需要管理的代码文件夹，鼠标右键：`Git Bash Here`
> 先打开`Git Bash Here`再cd进入目标目录也可以


##### 1、设置签名

用户名、邮箱
> 签名的目的只是为了区别身份，只是告诉团队人员这是谁提交的代码，无他意，可不写邮箱都行，跟远程代码库账号无任何关系
>
> 如果签名仅限在当前仓库下使用，则后面不需要加global，如果签名在当前电脑系统账号下的所有仓库下使用，则需要添加global，两类账号可以同时都设置

命令：
```
git config --global user.name 用户名
git config --global user.email 邮箱
```
> 如果不加global，则将信息保存在当前仓库`.git\config`文件内
>
> 如果是全局账号，则将信息保存在`C:\Users\Administrator\.gitconfig`文件内
> ```
> [user]
> 	name = 用户名
> 	email = 邮箱
> ```

##### 2、初始化本地仓库：

命令：
```git init```

会在当前目录下生成一个 **.git** 文件夹（不要随便修改和删除）

##### 3、查看仓库状态

命令：
```
git status
```
> track：让git追踪管理仓库
>
> 如果是首次提交，则显示：`new file：文件名`
>
> 如果提交修改过的文件，则显示：`modified: 文件名`

##### 4、提交到暂存区

命令：
```
git add 文件名
```
> 未添加到暂存去的文件为红色，已添加的为绿色
>
> 从暂存区删除已提交的文件：
>
> 首次提交，必须用`git add`提交到暂存库，非首次则可以直接用`git commit`提交到版本库
>
> 撤销新文件提交：`git rm --cacahed 文件名`
>
> 成效已更新文件的提交：`git reser HEAD 文件名`

##### 5、提交到代码库

命令：
```
git commit 文件名
```
点击确认后，开始提交，并会自动打开.git/git/COMMIT_EDITMSG[+]文件的vim编辑状态

该文件是本次提交代码的说明

直接输入或者`i`进入输入模式，在第一行填写本次修改的说明文字，然后按`ESC`退出输入模式，并进入命令模式，输入`:wq`保存并退出，`:q`退出(未修改内容)，`:q!`强制退出(修改过内容)

**可以在命令里面提交说明文字：`git commit -m "内容" 文件名`**

> master (root-commit), master是分支，root-commit是根提交

#### 提交到远程库（github等）

##### 1、创建一个远程仓库

登录gihub，然后点击右上角加号，选择new repository，打开创建仓库页面
> 
> 1、填写仓库名称(数字字母)
> 
> 2、添加仓库描述（可不填写）
> 
> 3、选择共有私有
> 
> 4、选择是否自动生成一个README文件（可不选）

##### 2、将远程仓库绑定到本地

复制远程仓库的https地址（进入新建的仓库里面可以看到）：https://github.com/aixinme/gitest.git

打开git bash客户端：

`git remote add 别名 远程库地址`

这样就在本地给远程库创建了别名，然后：

`git remote -v` 查看已创建的远程库别名

就可以看到：
```
别名 远程库 (fetch)
别名 远程库 (push)
```

fetch是获取远程仓库，push是推送到远程仓库

##### 3、将本地仓库推送带远程

`git push 远程仓库别名 本地仓库分支名称`

#### 克隆远程库

进入本地仓库，直接在bash里面输

`git clone 远程仓库克隆地址` 

> 1. 下载完整的代码
> 2. 创建远程库别名
> 3. 初始化本地库

要重新提交到远程库时，需要管理源授权


#### Phpstorm继承git

File -> Setting -> Version Control -> Git(设置git本地路径，默认即可)

File -> Setting -> Version Control -> Github(输入账号密码登录)

VCS -> Import Into Version Control -> Create Git Repository(创建git仓库，即初始化本地仓库)

选择需要上传的文件，右键 -> git -> commit，
如果是第一次上传，需要先git add

VCS -> Import Into Version Control -> Share Project on Github(将本地库上传到gihub)
输入远程库名称，选择公有私有，填写别名 填写描述（可不写）
