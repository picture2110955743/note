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
> 【remote repository】远程仓库，适合协作，成员之间共享资料，也适合自己云存储
>
> 提交流程：工作区 > 暂存区 (git add) > 本地仓库 (git commit) >远程仓库( )

| 命令                 | 作用                                                         |
| -------------------- | ------------------------------------------------------------ |
| git init             | 初始化本地仓库(会生成.git的文件夹)                           |
| git clone < url>     | 克隆远程版本库到工作区中。                                   |
| git add < file>      | 跟踪指定的文件，将工作区放到暂存区(参数可以是目录或单个多个文件) |
| git status           | 查看状态(暂存区和工作区那些文件没有提交)                     |
| git diff             | 查看变更内容（查看修改了那些内容）                           |
| git commit -m "注释" | 将暂存区文件提交到本地仓库，不指定注释会弹出文本编辑器       |