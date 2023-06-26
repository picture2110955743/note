## 一、安装

> 官网：https://git-scm.com/
>
> 证明：右击快捷菜单有Git GUL Here 和 Git Bash Code两个属性就可以了。

### 1.配置

介绍：因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址

- 修改

  > --global：添加此选项表示修改所有的仓库信息，如果取出掉表示只修改当前库的信息

  | 命令                                  | 作用       |
  | ------------------------------------- | ---------- |
  | git config --global user.name "~"     | 修改用户名 |
  | git config --global user.password "~" | 修改秘密   |
  | git config --global user.email "~"    | 修改邮箱   |

- 查看

  | 命令                     | 作用         |
  | ------------------------ | ------------ |
  | git config user.name     | 查看用户名   |
  | git config user.password | 查看密码     |
  | git config user.email    | 查看邮箱     |
  | git config --list        | 查看配置信息 |

### 2.取消代理

介绍：提交到远程仓库报错的时候因为代理原因可以取消git的http代理

```git
//报错信息
fatal: unable to access 'https://github.com/xxx/autowrite.git/': 
OpenSSL SSL_read: Connection was reset, errno 10054
或
fatal: unable to access 'https://github.com/xxx/autowrite.git/':
Failed to connect to github.com port 443: Timed out
```

| 取消http或https的代理                   |
| --------------------------------------- |
| git config --global --unset http.proxy  |
| git config --global --unset https.proxy |

## 二、工作区、暂存区、本地库

![入图所示](C:\Users\leng\Desktop\第四代笔记\assc\其他程序\GIT\1.png)

> 【workspace】工作区，日常写代码的文件夹
>
> 【staging area】暂存区，中介阶段，临时存放内容的地方
>
> 【local repository】本地库/版本库，提交到代码库，并且增加了历史操作内容，适合个人
>
> 说明：提交到本地库就需要添加用户名、密码和邮箱了。
>
> 【remote repository】远程仓库，适合协作，成员之间共享资料，也适合自己云存储
>
> 提交流程：工作区 > 暂存区 (git add) > 本地仓库 (git commit) >远程仓库( git push )

| 命令                 | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| git init             | 初始化本地仓库(会生成.git的文件夹)                           |
| git clone < url>     | 克隆远程版本库到工作区中。                                   |
| git add < file>      | 跟踪指定的文件，将工作区放到暂存区(参数可以是目录或单个多个文件) |
| git status           | 查看状态(暂存区和工作区那些文件没有提交)                     |
| git diff             | 查看变更内容（查看修改了那些内容）                           |
| git commit -m "注释" | 将暂存区文件提交到本地仓库，不指定注释会弹出文本编辑器       |

### 1.设置分支

| 命令                     | 说明                       |
| ------------------------ | -------------------------- |
| git branch [分支名称]    | 创建分支                   |
| git branch -d [分支名称] | 删除分支                   |
| git branch -v            | 产看分支                   |
| git checkout [分支名称]  | 切换分支                   |
| git merge [指定分支名称] | 将指定的分支合并到本分支中 |

> 合并并不仅仅是简单的文件添加、移除的操作，Git 也会合并修改。
>
> 修改一个文件内容合并后会有冲突，这时候就需要手动打开文件，进行调整了

### 2.远程仓库

| 命令                                               | 说明                                 |
| -------------------------------------------------- | ------------------------------------ |
| git remote add < 别名> < 远程仓库地址url>          | 添加远程仓库并指定别名               |
| git remote                                         | 列出所有仓库的别名                   |
| git remote -v                                      | 查看远程仓库的信息                   |
| git remote show < 别名>                            | 查看指定别名的远程仓库信息           |
| git push -u < 别名> < 分支>                        | 将本地仓库上传到远程仓库（并且合并） |
| git push --tags                                    | 上传所有标签                         |
| git pull < 远程主机名> < 远程分支名>:< 本地分支名> | 下载远程仓库到本地仓库               |
| git fetch < 远程仓库名>                            | 下载远程仓库到本地仓库               |

> git pull 和 git fetch 的区别
>
> （1）pull是直接把下载的文件合并到本地分支，而fetch是下载后选择要不要合并
>
> （2）git fetch下载后需要执行git merge [指定分支名称]语句来进行合并
>
> ![](C:\Users\leng\Desktop\第四代笔记\assc\其他程序\GIT\5.png) 

### 3.标签

介绍：下载远程仓库到本地仓库版本信息是一串数字不好看，但是添加标签后就表号看

| 命令              | 作用           |
| ----------------- | -------------- |
| git tag   "内容"  | 添加标签       |
| git tag -d ”内容“ | 删除指定的标签 |
| git tag           | 产看所有标签   |

### 4.删除和撤销

| 命令                            | 作用                                               |
| ------------------------------- | -------------------------------------------------- |
| git mv [-f]  <文件名> < 新名字> | 将工作区的文件重命名(新文件名已经存在时需要加上-f) |
| git mr [-f] [-cached] < file>   | 查看提交的历史(git commit提交的记录)               |
| git checkout HEAD < file>       | 撤销指定的未提交文件的修改内容                     |
| git reset [~] HEAD              | 撤销工作目录中所有未提交的文件和修改的内容         |

> 【git mr】强行删除两个区的文件需要加上-f参数，如果只删除暂存区保留工作区的文件，就是从跟踪清单中删除，添加上-cacheed参数
>
> 【git reset】的参数：
>
> （1）--mixed：默认可以不带参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变
>
> （2）--soft：参数用于回退到某个版本
>
> （3）--hard 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交：
>
> - HEAD参数可以是：HEAD当前版本、HEAD^上一个版本，HEAD^^上上个版本，以此类推
>
> - 也可以是：HEAD0当前版本，HEAD1上一个版本以此类推
>
> - 也可以是版本号

### 5.查看历史文件

| 命令               | 说明                                 |
| ------------------ | ------------------------------------ |
| git log            | 查看提交的历史(git commit提交的记录) |
| git log -p < file> | 查看指定文件的历史                   |
| git blame < file>  | 以列表方式查看指定文件的历史         |

> git log参数：
>
> (1) git log -pretty=oneline
>
> ![](C:\Users\leng\Desktop\第四代笔记\assc\其他程序\GIT\2.png) 
>
> (2) git log --oneline（简洁）
>
> ![](C:\Users\leng\Desktop\第四代笔记\assc\其他程序\GIT\3.png) 
>
> (3) 数 git reflog（HEAD@{版本号得出移动到该版本需要多少步数}
>
>  ![](C:\Users\leng\Desktop\第四代笔记\assc\其他程序\GIT\4.png)



## 其他、命令速查表

![](C:\Users\leng\Desktop\第四代笔记\assc\其他程序\GIT\6.png)

