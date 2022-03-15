---
title: SpringBoot
date: 2022-03-06
tags:
    - git
---

> 申明，本教程使用 Intellij IDEA 作为 java 开发环境，该教程仅提供学习，如需使用、转载文章请联系博主，未经授权严禁转载。

<!--more-->

> **视频教程：**
>
> 【尚硅谷】5h打通Git全套教程丨2021最新IDEA版 https://www.bilibili.com/video/BV1vy4y1s7k6

# 课程目录

- Git

  > Git介绍	分布式版本控制工具  VS  集中式版本控制工具
  >
  > Git安装	基于官网发布的最新版本 2.31.1 安装详解
  >
  > Git命令	基于开发案例，详细讲解了 git 的常用命令
  >
  > Git分支	分支特性	分支创建	分支转换	分支合并	代码合并冲突解决
  >
  > Idea 集成 Git 	

- GitHub

  > 创建远程库
  >
  > 代码推送	Push
  >
  > 代码拉取	Pull	
  >
  > 代码克隆	Clone
  >
  > SSH免密登录
  >
  > Idea 集成 GitHub

- Gitee码云

  > 码云创建远程库
  >
  > Idea集成Gitee码云
  >
  > 码云连接GitHub 进行代码的复制和迁移

- GitLab

  > GitLab服务器的搭建和部署
  >
  > Idea集成GitHub



## 上传GitHub常用命令总结（🔴🟡）

> 以下操作命令按顺序执行即可。
>
> 需要对后面命令有所了解。

### 1）将代码上传到 `master` 分支（旧）

| **命令**                                      | **说明**                                         |
| --------------------------------------------- | ------------------------------------------------ |
| `git init`                                    | 工作空间创建 `.git` 文件夹（默认隐藏了该文件夹） |
| `git add .`                                   | 添加到暂存区                                     |
| `git commit -m "你的提交注释注释"`            | 提交到本地库                                     |
| `git remote add origin http://xxxxxxxxx.git ` | 本地仓库和远程 github 关联（别名：origin）       |
| `git pull --rebase origin master`             | 远程仓库有 .md 文件，拉取到本地库                |
| `git push -u origin master`                   | 代码合并（第一次提交不需要 -u ）                 |

### 2）将代码上传到默认`main`分支（新）

| **命令**                                      | **说明**                                          |
| --------------------------------------------- | ------------------------------------------------- |
| `git --version`                               | 查看版本                                          |
| `git config --global init.defaultBranch main` | `git`在`2.28.0`上，重新设置 `git`默认分支为`main` |
| `git init`                                    | 工作空间创建`.git`文件夹（默认隐藏了该文件夹）    |
| `git add .`                                   | 添加到暂存区                                      |
| `git commit -m "你的提交注释注释"`            | 提交到本地库                                      |
| `git remote add origin http://xxxxxxxxx.git`  | 本地仓库和远程 github 关联（别名：origin）        |
| `git pull --rebase origin main`               | 远程仓库有 .md 文件，拉取到本地库                 |
| `git push -u origin main`                     | 代码合并（第一次提交不需要 -u ）                  |





## 一、Git 概述

> Git 是一个免费的、开源的**分布式版本控制系统**，可以高效地处理从小型到大型的各种项目。
>
> Git 易于学习，占地面积小，性能极快。它具有廉价的本地库，方便的暂存区域和多个工作流分支特性。其性能优于Subversion、CVS、Perforce和ClearCase 等版本控制工具。



### 1）git 工作机制

![image-20220226141843926.png](https://s2.loli.net/2022/02/26/QEFWquNAJpfwGBg.png)







### 2）Git 和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般我们简单称为**远程库**。

- 局域网
  - GitLab

- 互联网
  - GitHub（网外）
  - Gitee 码云（国内）



## 二、Git 安装

参考官方文档：https://git-scm.com/book/zh/v2/

安装流程一般就是傻瓜式安装。



## 三、Git 常用命令（🔴🟡）

|               命令名称               |        作用        |
| :----------------------------------: | :----------------: |
| git config --global user.name 用户名 |    设置用户签名    |
| git config --global user.email 邮箱  |    设置用户签名    |
|             **git init**             |  **初始化本地库**  |
|            **git status**            | **查看本地库状态** |
|          **git add 文件名**          |  **添加到暂存区**  |
| **git commit -m "日志信息" 文件名**  |  **提交到本地库**  |
|            **git reflog**            |  **查看历史记录**  |
|     **git reset --hard 版本号**      |    **版本穿梭**    |

- 查看设置的用户签名

![image-20220226182908172.png](https://s2.loli.net/2022/02/26/wfuh3KjD5IisSN6.png)

**说明：**

​	签名的作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息中能够看到，以此来确定本次提交是谁做的。**Git 首次安装必须设置一下用户签名，否则无法提交代码。**

> **注意**：这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系。



### 1）初始化本地库

> 基本语法：git init

案例实操：

- 使用git进入到你想要操作的目录或者在此目录下右键git进入。

- 执行 git init 命令

- 在此目录下会出现一个 .git 文件夹（隐藏的）

  ![image-20220226184325066.png](https://s2.loli.net/2022/02/26/uXiea4O3lUfSsR5.png)

![image-20220226190452180.png](https://s2.loli.net/2022/02/26/pO1LHfGb2wSEMea.png)

![image-20220226191021785.png](https://s2.loli.net/2022/02/26/eaGHpfvWXE9O57P.png)

![image-20220226191932714.png](https://s2.loli.net/2022/02/26/yhFS1rxVCODUBwG.png)

> 注意：
>
> 一般仓库的名称路径都选用英文，此图不标准。



## 四、Git 分支操作

![image-20220226192716037.png](https://s2.loli.net/2022/02/26/YojNq5QtxzHyvKw.png)

### 1）分支的好处？

同时并行多个功能开发，提高开发效率。

各个分支在开发过程中，如果有一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。

### 2）分支的操作常用命令（🔴🟡）

|      命令名称       |             作用             |
| :-----------------: | :--------------------------: |
|  git branch 分支名  |           创建分支           |
|    git branch -v    |           查看分支           |
| git checkout 分支名 |           切换分支           |
|  git merge 分支名   | 把指定的分支合并到当前分支上 |

![image-20220226193544177.png](https://s2.loli.net/2022/02/26/yLHIYiR6329SkaK.png)



### 3）git merge 产生冲突

- 产生冲突的原因：是不知道到底保存哪一个分支的内容。

- 解决方法：手动去改变产生冲突的内容。



### 4）创建分支和切换分支的图解

![image-20220226194913635.png](https://s2.loli.net/2022/02/26/5GqzjTbdExiB1SH.png)

> master、dev1 其实都是指向具体版本记录的指针。当前所在的分支，其实是由 HEAD决定的。所以创建分支的本质就是多创建一个指针。
>
> HEAD 如果是指向 master，那么我呢吧现在就是在 master 分支上。
>
> HEAD 如果是指向 dev1，那么我呢吧现在就是在 dev1分支上。
>
> **所以切换分支的本质：就是移动 HEAD 指针。**



## 五、Git团队协作

### 1）团队内协作

![image-20220226195423081.png](https://s2.loli.net/2022/02/26/5EQsh2KRyYFaWVL.png)

### 2）跨团队协作

![image-20220226195442497.png](https://s2.loli.net/2022/02/26/u3ncm2iIoyPlX84.png)



## 六、GitHub操作

### 1）推送和拉取

- 去 github 上创建一个仓库
- 复制仓库的 https 连接
- 修改别名

![image-20220226200620552.png](https://s2.loli.net/2022/02/26/mqt3javlSRIzn8N.png)

推送到远程仓库：

- `git push [仓库别名/链接] 分支名`

拉取到本地（更新本地库）：

- `git pull [仓库别名/链接] 分支名`



### 2）克隆

`git clone [仓库链接地址]`

- 拉取代码
- 初始化本地仓库
- 创建别名



### 3）邀请团队内成员协作开发

- 远程库的 settings 栏下 Collaborators 可以添加协作者

  ![image-20220226203101837.png](https://s2.loli.net/2022/02/26/PgXQKxU8ASpd631.png)





### 4）团队外成员协作

![image-20220226204118728.png](https://s2.loli.net/2022/02/26/uQbSM5eq6HJnoLw.png)



### 5）SSH 免密登录



## 七、IDEA集成 Git

### 1）忽略无关文件

![image-20220226204755560.png](https://s2.loli.net/2022/02/26/jbsPely5kTdz4Qt.png)



#### 忽略原因：

- 与项目的实际功能无关，不参与服务器部署运行。把它们忽略掉能够屏蔽 IDE 工具之间的差异。

#### 如何忽略？

- 创建忽略规则文件 xxxx.ignore（前缀名随便起，建议是 git.ignore）

  这个文件的存放位置原则上在哪里都可以，为了便于让 ~/.gitconfig 文件引用，建议也放在用户家目录下

- git.ignore 文件模板内容如下：

  ```ignore
  # Complied class file
  *.class
  
  # Log file
  *.log
  
  # BlueJ files
  *.ctxt
  
  # Mobile Tools for Java(J2ME)
  .mtj.tem/
  
  # Package Files #
  *.jar
  *.war
  *.nar
  *.ear
  *.zip
  *.tar.gz
  *.rar
  
  #  virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
  hs_err_pid*
  
  .classpath
  .project
  .settings
  target
  .idea
  *.iml
  
  ```

- 在 .gitconfig 中添加

  ```gitconfig
  [user]
  	name = Pnawei
  	email = 2191395534@qq.com
  [core]
  	autocrlf = false
  	excludesfile = [这里添加的git.ignore所放在的目录位置]
  ```

  

### 2）定位 Git  程序

![image-20220226210738212.png](https://s2.loli.net/2022/02/26/QYjftPCHoReybAv.png)



### 3）初始化本地库 

![image-20220226210932347.png](https://s2.loli.net/2022/02/26/CfexsuZvclapmwD.png)



### 4）提交本地库

![image-20220226211425327.png](https://s2.loli.net/2022/02/26/7Fe1w5iBtpxnR36.png)



### 5）版本控制

![image-20220226211703759.png](https://s2.loli.net/2022/02/26/BCvf45DrJVmNSa6.png)

切换版本：

- 直接右键 操作选择 checkout 



### 6）创建分支、切换分支

方法一：

![image-20220226211840026.png](https://s2.loli.net/2022/02/26/tzTrSudsK2ikpC4.png)



方法二： 点击右下角的分支即可

![image-20220226211959363.png](https://s2.loli.net/2022/02/26/LlNFIxv85B7YSV6.png)



切换如图方法二。



### 6）合并分支

### 7）冲突合并

![image-20220226212730288.png](https://s2.loli.net/2022/02/26/iJrVdLWQTkjXghc.png)





## 八、IDEA集成 GitHub

配置 GitHub 插件，如果 idea 中没有

### 1）添加 GitHub 账号

![image-20220226212747959.png](https://s2.loli.net/2022/02/26/OAQPdsjVDkCZJ8t.png)



### 2） push 推送本地库到远程库

右键点击项目，可以将当前分支的内容 push 到 GitHub 的远程仓库中。

![image-20220226213310216.png](https://s2.loli.net/2022/02/26/Cifl8vakxBQyOEN.png)



### 3）pull 拉取远程库到本地库

右键点击项目，可以将远程库的内容 pull 到本地仓库

![image-20220226213634556.png](https://s2.loli.net/2022/02/26/dzoAZKenIGNlcby.png)



### 4）clone 克隆远程库到本地 （正常来说不需要）

![image-20220226213719160.png](https://s2.loli.net/2022/02/26/GWUPf6vJALi7cMo.png)



## 九、国内代码托管中心-码云

操作跟 GitHub 如出一辙。

码云官网：https://gitee.com/





## 十、自建代码托管平台-GitLab

![image-20220226214126152.png](https://s2.loli.net/2022/02/26/s9XLwvqlYk7UGzm.png)

![image-20220226214104786.png](https://s2.loli.net/2022/02/26/Ll8s5aEfkAJudFo.png)