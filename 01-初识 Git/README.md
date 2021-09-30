> 笔记来源：[【尚硅谷】5h打通Git全套教程IDEA版（涵盖GitHub\Gitee码云\GitLab）](https://www.bilibili.com/video/BV1vy4y1s7k6)

[TOC]

# 初识 Git

## 0、内容介绍

### Git

- Git 介绍：分布式版本控制工具 VS 集中式版本控制工具
- Git 安装：基于官网发布的最新版本 2.31.1 安装讲解
- Git 命令：基于开发案例详细讲解了`git`的常用命令
- Git 分支：分支特性、分支创建、分支转换、分支合并、代码合并冲突解决
- IDEA 集成 Git

### GitHub

- 创建远程库
- 代码推送 Push
- 代码拉取 Pull
- 代码克隆 Clone
- SSH 免密登录
- IDEA 集成 GitHub

### Gitee 码云

- 创建远程库
- IDEA 集成 GitHub
- 码云连接 GitHub 进行代码的复制和迁移

### GitLab

- GitLab 服务器的搭建和部署
- IDEA 集成 GitLab



## 1、Git 概述

- 官网地址：[http://git-scm.com/](http://git-scm.com/)
- `--everything is local`：分布式特性

Git 是一个**免费**的、**开源**的 <mark>分布式版本控制系统</mark>，可以快速高效地处理从小型到大型的各种项目

Git 易于学习，占地面积小，**性能极快**。它具有廉价的本地库，方便的暂存区域和多个工作流分支等特性

其性能优于 Subversion、CVS、Perforce 和 ClearCase 等版本控制工具

### 1.1、何为版本控制？

版本控制是一种记录文件内容变化，以便将来查阅特定版本修订情况的系统

版本控制其实最重要的是可以记录文件修改**历史记录**，从而让用户能够查看历史版本，方便版本切换

![image-20210916222911720](https://i.loli.net/2021/09/16/6NizZtSKQLWrjw2.png)

### 1.2、为什么需要版本控制？

个人开发过渡到团队协作

![image-20210916223038071](https://i.loli.net/2021/09/16/QfoYW7w6LdKzJrc.png)

### 1.3、版本控制工具

#### 集中式版本控制工具

CVS、SVN（Subversion）、VSS.......

集中化的版本控制系统诸如 CVS、SVN 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。多年以来，这已成为版本控制系统的标准做法

这种做法带来了许多好处，每个人都可以在一定程度上看到项目中的其他人正在做些什么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个集中化的版本控制系统，要远比在各个客户端上维护本地数据库来得轻松容易

事分两面，有好有坏。这么做显而易见的缺点是中央服务器的单点故障。如果服务器宕机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作

![image-20210916223444358](https://i.loli.net/2021/09/17/jJYo2bAwSIHkG4B.png)

**总结**

- **优点**：可以看到其他人正在做些什么；开发者权限控制
- **缺点**：中央服务器的单点故障，无法提交历史记录

#### 分布式版本控制工具

Git、Mercurial、Bazaar、Darcs.......

像 Git 这种分布式版本控制工具，客户端提取的不是最新版本的文件快照，而是把代码仓库完整地镜像下来（本地库）。这样任何一处协同工作用的文件发生故障，事后都可以用其他客户端的本地仓库进行恢复。因为每个客户端的每一次文件提取操作，实际上都是一次对整个文件仓库的完整备份

分布式的版本控制系统出现之后，解决了集中式版本控制系统的缺陷：

1. 服务器断网的情况下也可以进行开发（因为版本控制是在本地进行的）
2. 每个客户端保存的也都是整个完整的项目（包含历史记录，更加安全）

![image-20210916224708069](https://i.loli.net/2021/09/16/6rPsyHajdgDB2TO.png)

**优点**：

- 版本控制在本地，可以断网开发
- 保存完整项目，包含历史记录，更安全

### 1.4、Git 简史

![image-20210916225109044](https://i.loli.net/2021/09/17/D4uGkUECizseawt.png)

### 1.5、Git 工作机制

![image-20210916225215882](https://i.loli.net/2021/09/16/EzVI3GWPdQ9wc17.png)

- **工作区**写代码，通过`git add`命令添加至**暂存区**
- **暂存区**临时存储代码，通过`git commit`提交至**本地库**
- **本地库**记录历史记录，通过`git push`推送至**远程库**

### 1.6、Git 和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般我们简单称为**远程库**

- 局域网
  - :ballot_box_with_check: GitLab
- 互联网
  - :ballot_box_with_check: GitHub（外网）
  - :ballot_box_with_check: Gitee码云（国内网站）



## 2、Git 安装

---

官网地址：[https://git-scm.com/](https://git-scm.com/)

查看 GNU 协议，可以直接点击下一步

![image-20210916233221530](https://i.loli.net/2021/09/16/CVxgLzDO8mjXdSK.png)

选择 Git 安装位置，要求是非中文并且没有空格的目录，然后下一步

![image-20210916233242454](https://i.loli.net/2021/09/16/ckTh61JGiPXD8lW.png)

Git 选项配置，推荐默认设置，然后下一步

![image-20210916233256977](https://i.loli.net/2021/09/17/eBrqf6NHFyIpjOR.png)

Git 安装目录名，不用修改，直接点击下一步

![image-20210916233310729](https://i.loli.net/2021/09/17/WcbXGyrYmgVM7Ih.png)

Git 的默认编辑器，建议使用默认的 Vim 编辑器，然后点击下一步

![image-20210916233417531](https://i.loli.net/2021/09/17/jatAiNHho6FTzxs.png)

默认分支名设置，选择让 Git 决定，分支名默认为 master，下一步

![image-20210916233436237](https://i.loli.net/2021/09/17/Sjn9kC586dvAghx.png)

修改 Git 的环境变量，选第一个，不修改环境变量，只在 Git Bash 里使用 Git

![image-20210916233458071](https://i.loli.net/2021/09/17/pfDUIHwAQ1jyza7.png)

选择后台客户端连接协议，选默认值 OpenSSL，然后下一步

![image-20210916233517370](https://i.loli.net/2021/09/17/wmqydKAvuelRkEf.png)

配置 Git 文件的行末换行符，Windows 使用 CRLF，Linux 使用 LF，选择第一个自动转换，然后继续下一步

![image-20210916233531902](https://i.loli.net/2021/09/17/7C8hQ3PH5c4vEaD.png)

选择 Git 终端类型，选择默认的 Git Bash 终端，然后继续下一步

![image-20210916233717491](https://i.loli.net/2021/09/17/dHz2iXnJt49KwjM.png)

选择 Git pull 合并的模式，选择默认，然后下一步

![image-20210916233746777](https://i.loli.net/2021/09/17/WSrhmtwcQyNJdDs.png)

选择 Git 的凭据管理器，选择默认的跨平台的凭据管理器，然后下一步

![image-20210916233757028](https://i.loli.net/2021/09/17/Rodj7rIZHEMU5SC.png)

 其他配置，选择默认设置，然后下一步

![image-20210916233804540](https://i.loli.net/2021/09/17/FwjEBZl4SAruhxs.png)

实验室功能，技术还不成熟，有已知的 bug，不要勾选，然后点击右下角的 Install 按钮，开始安装 Git

![image-20210916233812916](https://i.loli.net/2021/09/17/2zfiKg4WpwCq9YL.png)

点击 Finsh 按钮，Git 安装成功！

![image-20210916233821255](https://i.loli.net/2021/09/17/KWEZ9AYD1NbcX7g.png)

右键任意位置，在右键菜单里选择 Git Bash Here 即可打开 Git Bash 命令行终端

![image-20210916233913106](https://i.loli.net/2021/09/17/ad7zuHvK2McTQl5.png)

在 Git Bash 终端里输入 `git --version` 查看 git 版本，如图所示，说明 Git 安装成功

![image-20210917000255009](https://i.loli.net/2021/09/17/OHZko9jdDWvRMKi.png)



## 3、Git 常用命令

| 命令                              | 作用           |
| :-------------------------------- | :------------- |
| `git config user.name 用户名`     | 设置用户签名   |
| `git config user.email 邮箱`      | 设置用户签名   |
| `git init`                        | 初始化本地库   |
| `git status`                      | 查看本地库状态 |
| `git add 文件名`                  | 添加至暂存区   |
| `git commit -m "日志信息" 文件名` | 提交至本地库   |
| `git reflog`                      | 查看历史记录   |
| `git reset --hard 版本号`         | 版本穿梭       |

### 3.1、设置用户签名

1）基本语法

```bash
git config --global user.name 用户名
git config --global user.email 邮箱
```

2）案例实操

全局范围的签名设置

![image-20210917001235229](https://i.loli.net/2021/09/17/62JueaM9ByrmHdX.png)

说明： 

签名的作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息中能够看到，以此确认本次提交是谁做的

<mark>Git 首次安装必须设置一下用户签名，否则无法提交代码</mark>

:bangbang: 注意：这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系

### 3.2、初始化本地库

1）基本语法

```bash
git init
```

2）案例实操

![image-20210917203400924](https://i.loli.net/2021/09/17/QBPNgHCUzGOiJuy.png)

### 3.3、查看本地库状态

1）基本语法

```bash
git status
```

2）案例实操

![git status](https://i.loli.net/2021/09/17/b645MnGSFxRyhaQ.gif)

新增文件前

![image-20210917204804510](https://i.loli.net/2021/09/17/4xCVHGPLgjXbB1F.png)

新增文件后

![image-20210917204858689](https://i.loli.net/2021/09/17/IqK6GEc92hYx7HF.png)

###  3.4、添加暂存区

1）基本语法

```bash
git add 文件名
```

2）案例实操

红色表示仍在工作区，修改尚未被追踪；绿色表示已添加至暂存区，修改被追踪

![image-20210917205319556](https://i.loli.net/2021/09/17/DnfmIo3KZlt5zJ4.png)

使用命令，删除暂存区该文件（只是删除暂存区，不影响工作区）

```bash
git rm --cached hello.txt
```

![image-20210917205546165](https://i.loli.net/2021/09/17/uJS8Gp3CazAKU7l.png)

### 3.5、提交至本地库

1）基本语法

```bash
# -m 表示添加一个版本日志信息，不写此参数也会打开日志信息的文件框。一般带参数
git commit -m "日志信息" 文件名
```

2）案例实操

正常操作

![image-20210917210542226](https://i.loli.net/2021/09/17/KNfMvCTkE3YQxdj.png)

无`-m`参数时

![image-20210917210109185](https://i.loli.net/2021/09/17/bvTfga13wtuSUhq.png)

如果强制退出

![image-20210917210156460](https://i.loli.net/2021/09/17/XIx7L3lTW9FcBtP.png)

### 3.6、修改文件

案例实操

![image-20210917211143162](https://i.loli.net/2021/09/17/o2p7dO4F9A5VDjJ.png)

git 里是按照行维护文件的，所以修改内容其实就是之前的行删除，修改过后的行添加进来

因此在`commit`之后提示信息`1 insertion(+), 1 deletion(-)`

### 3.7、历史版本

#### 查看历史版本

1）基本语法

```bash
# 查看精简版本信息
git reflog
# 查看详细版本信息
git log
```

2）案例实操

![image-20210917211945690](https://i.loli.net/2021/09/17/p2mvTbZuEqVkYB9.png)

#### 版本穿梭

1）基本语法

```bash
git reset --hard 版本号
```

2）案例实操

![image-20210917212348218](https://i.loli.net/2021/09/17/nBw6OEL9liyMe7d.png)

文件验证当前版本号

![image-20210917212941200](https://i.loli.net/2021/09/17/vMYXFVyWo6PNOzf.png)

Git 切换版本，底层其实是移动的 HEAD 指针，具体原理如下图所示

![image-20210917213424162](https://i.loli.net/2021/09/17/5GQRnhD8XijVZuy.png)

![image-20210917213247141](https://i.loli.net/2021/09/17/CVdReJPu5YMTmHQ.png)

![image-20210917213333350](https://i.loli.net/2021/09/17/oU5ORWqvghNCcTi.png)



## 4、Git 分支操作

![image-20210917213616760](https://i.loli.net/2021/09/17/6jGfxUmrERZSV9h.png)

### 4.1、什么是分支

在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支。使用分支意味着程序员可以把自己的工作从开发主线上分离开来，开发自己分支的时候，不会影响主线分支的运行。对于初学者而言，分支可以简单理解为副本，一个分支就是一个单独的副本（分支底层其实也是指针的引用）

![image-20210917213935209](https://i.loli.net/2021/09/17/AVwpC1ZLzmOlEUg.png)

### 4.2、分支的好处

同时并行推进多个功能开发，**提高开发效率**

各个分支在开发过程中，如果某一个分支开发失败，**不会对其他分支有任何影响**。失败的分支删除重新开始即可

### 4.3、分支的操作

| 命令                  | 作用                       |
| :-------------------- | :------------------------- |
| `git branch 分支名`   | 创建分支                   |
| `git branch -v`       | 查看分支                   |
| `git checkout` 分支名 | 切换分支                   |
| `git merge` 分支名    | 把指定的分支合并到当前分支 |

#### 创建分支、查看分支

1）基本语法

```bash
git branch 分支名
git branch -v
```

2）案例实操

![image-20210917214653546](https://i.loli.net/2021/09/17/PVOR9ZjmIqkr4cv.png)

#### 切换分支

1）基本语法

```bash
git checkout 分支名
```

2）案例实操

![image-20210917215246415](https://i.loli.net/2021/09/17/AR9NuTBG2UweEnb.png)

#### 合并分支

1）基本语法

```bash
git merge 分支名
```

2）案例实操

**正常合并**

![image-20210917215908842](https://i.loli.net/2021/09/17/UcwRJu78Kmvod4k.png)

**冲突合并**

冲突产生的原因：合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改。Git无法替我们决定使用哪一个。必须人为决定新代码内容

![image-20210917220923478](https://i.loli.net/2021/09/17/gcnCSJKtNqrokIQ.png)

解决冲突

![image-20210917221121233](https://i.loli.net/2021/09/17/mU3Y9JodyTpV7nB.png)

![image-20210917221239011](https://i.loli.net/2021/09/17/S6OrkKeFsCymWcB.png)

![image-20210917222018377](https://i.loli.net/2021/09/17/iMQfWOwkSH8ujh2.png)

#### 创建分支和切换分支图解

![image-20210917221451896](https://i.loli.net/2021/09/17/6WNlEc9FbaJmhkv.png)

![image-20210917221515718](https://i.loli.net/2021/09/17/OKwIG2BvZC7mVjl.png)

master、hot-fix 其实都是指向具体版本记录的指针。当前所在的分支，其实是由 HEAD 决定的。所以创建分支的本质就是多创建一个指针

- HEAD 如果指向 master，那么我们现在就在 master 分支上
- HEAD 如果指向 hotfix，那么我们现在就在 hotfix 分支上

所以切换分支的本质就是移动HEAD指针



## 5、Git 团队协作机制

### 5.1、团队内协作

![image-20210917222216595](https://i.loli.net/2021/09/17/HWlevFmCKdRju6V.png)

### 5.2、跨团队协作

 ![image-20210917222441407](https://i.loli.net/2021/09/17/gvmsB4Rn7xYfc9A.png)



## 6、GitHub 操作

- GitHub 官网：[https://github.com/](https://github.com/)

PS：全球最大同性交友网站，技术宅男的天堂，新世界的大门，你还在等什么？

| 账号                 | 姓名       | 验证邮箱                     |
| :------------------- | :--------- | :--------------------------- |
| `atguiguyuebuqun`    | `岳不群`   | `atguiguyuebuqun@aliyun.com` |
| `atguigulinghuchong` | `令狐冲`   | `atguigulinghuchong@163.com` |
| `atguigudongfang1`   | `东方不败` | `atguigudongfang1@163.com`   |

### 6.1、创建远程仓库

![image-20210917223235275](https://i.loli.net/2021/09/17/iP9EZnU81O3wGYB.png)

![](https://i.loli.net/2021/09/17/gLQzrsRiN2Cj6Fe.png)

### 6.2、远程仓库操作

| 命令                               | 作用                                                     |
| :--------------------------------- | :------------------------------------------------------- |
| `git remote add 别名 远程地址`     | 起别名                                                   |
| `git remote -v`                    | 查看当前所有远程别名                                     |
| `git clone 远程地址`               | 将远程仓库的内容克隆到本地                               |
| `git pull 远程地址别名 远程分支名` | 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并 |
| `git push 别名 分支`               | 推送本地分支上的内容到远程仓库                           |

#### 创建远程仓库别名

1）基本语法

```bash
git remote -v
git remote add 别名 远程地址
```

2）案例实操

![image-20210917225451875](https://i.loli.net/2021/09/17/PfZBknlC8RjHvxV.png)

#### 推送本地分支到远程仓库

1）基本语法

```bash
git push 别名 分支
```

2）案例实操

由于 GitHub 外网的特殊原因，会有网络延迟，等待时间可能较长，属于正常现象。可能要多尝试几次，需要点耐心。当然你有工具除外

```bash
git push git-demo master
```

如果本地还没有过 SSH 免密登录操作（下面内容会详细介绍），则在执行命令后会弹出一个`Connect to GitHub`的提示框

![image-20210918224448045](https://i.loli.net/2021/09/18/27XoOIwArYdnhyE.png)

点击`Sign in with your browser`后会自动打开系统默认浏览器

如果你的 GitHub 尚未进行过任何 Git 相关授权，则会给出确认授权提示信息，点击`Authorize GitCredentialManager`进行授权即可

![image-20210918231341801](https://i.loli.net/2021/09/19/sOguJ7GYApZUiLS.png)

接着会提示授权成功（如果在此之前已经对`Git Credential Manager`进行过授权，则直接提示此信息）

![image-20210918224627107](https://i.loli.net/2021/09/18/clQsuFdDfemyxzR.png)

成功推送本地分支至远程库

![image-20210918224403240](https://i.loli.net/2021/09/18/ApuMYyt5S73LF6E.png)

**凭据管理器**

在上述操作过程中，点击`Authorize GitCredentialManager`进行授权后，在 GitHub 设置页面的`Application`选项—`Authorized OAuth Apps`中可以查看到 `Git Credential Manager`的授权信息

![image-20210918231735259](https://i.loli.net/2021/09/18/QgZLxhAM5fzis6n.png)

在上述过程前，本地凭据管理器中还没有任何身份凭证信息（没有 Git 和 GitHub 相关的凭据信息）

![image-20210918230512316](https://i.loli.net/2021/09/18/hBtO3EZJRnmWYeC.png)

执行过上述命令等操作后，本地凭据管理器中会出现 Git 相关凭据信息

![image-20210918233953904](https://i.loli.net/2021/09/19/nfe4SVwFj39JTuB.png)

#### 拉取远程仓库到本地

1）基本语法

```bash
git pull 别名 分支
```

2）案例实操

![image-20210918234422490](https://i.loli.net/2021/09/19/lqVRcoryfCZnMeg.png)

#### 克隆远程仓库到本地

1）基本语法

```bash
git clone 远程库地址
```

2）案例实操

首先获取需要克隆的远程库地址

![image-20210918235159899](https://i.loli.net/2021/09/18/V1s3vjWHUAiyIC2.png)

由于`workspace`下面已经存在一个同名的仓库地址，所以直接在`workspace`中键入命令会有错误提示信息

![image-20210918235519853](https://i.loli.net/2021/09/18/MIc5GEnqgrZsWBe.png)

这是因为，`clone`命令默认帮我们创建的一个远程仓库名称同名的文件夹，所以这里我删除了`git-demo`目录

![image-20210918235857263](https://i.loli.net/2021/09/19/LZYvpoBcJR56VlA.png)

小结：`clone` 会做如下操作

- 1、拉取代码
- 2、初始化本地仓库
- 3、创建别名（默认`origin`）

### 6.3、团队内协作

如果项目之外成员想要将自己编写的代码推送至远程库，则会提示`unable to access...403`

![image-20210919002334885](https://i.loli.net/2021/09/19/URnavcD49XsEkwY.png)

要想获取推送的权限，则需要该项目管理员对该成员进行邀请，将其添加至该项目中

1）邀请合作者，输入用户名，复制地址并发送给合作者

![image-20210919001646877](https://i.loli.net/2021/09/19/yHmSVrhQN5eFZow.png)

![image-20210919001732944](https://i.loli.net/2021/09/19/r6yLWmFxQVogejR.png)

![image-20210919001847491](https://i.loli.net/2021/09/19/p4qvjwdhcrSXM2R.png)

2）合作者访问该链接，点击接受邀请，可以在其账号上看到该远程仓库

- [https://github.com/atguiguvueyue/git-demo/invitations](https://github.com/atguiguvueyue/git-demo/invitations)

![image-20210919002022667](https://i.loli.net/2021/09/19/fxEsGzic2mgAJRt.png)

![image-20210919002239871](https://i.loli.net/2021/09/19/R9O3bTxLo7HfBw6.png)

接下来，就可以通过`git`命令对远程库进行克隆、拉取、提交、推送等操作了

### 6.4、跨团队协作

1）合作者视角

点击`Fork`，将其他项目“叉”到自己账号上

![image-20210919003412417](https://i.loli.net/2021/09/19/TzkfoeEVc5wi67d.png)

自己账号上就有了该项目，可以清楚地看到该项目`forked from xxx`，即可对代码进行修改

![image-20210919003500235](https://i.loli.net/2021/09/19/YzAaK6L4o8rx3Jw.png)

修改代码后，点击`Pull requests`—`New pull request`，发起拉取请求

![image-20210919004019396](https://i.loli.net/2021/09/19/UDezhHG5E7v93r1.png)

查看修改内容，点击`Create pull request`，创建拉取请求

![image-20210919004334829](https://i.loli.net/2021/09/19/rG3BDcENxJMot4R.png)

填写请求信息及评论内容，点击`Create pull request`

![image-20210919004505828](https://i.loli.net/2021/09/19/J8hZK1oVE2Hi9Gm.png)

创建完成

![image-20210919004830149](https://i.loli.net/2021/09/19/9kpVQfbAGz2gRL5.png)

2）项目管理员视角

可以在该项目中查看到`Pull requests`有一条新的记录，可以点击下方提交信息进行查看

![image-20210919005217558](https://i.loli.net/2021/09/19/nItWOHxSi9kleV5.png)

想要看到合作者修改的具体内容，可以点击提交记录进行查看

![image-20210919005303909](https://i.loli.net/2021/09/19/dOGxz6gusfM4onA.png)

![image-20210919005442954](https://i.loli.net/2021/09/19/54QENAfDJj3ikSl.png)

同时，可以对拉取请求进行审查和评论

![image-20210919005558618](https://i.loli.net/2021/09/19/385yrHgBX1uvPYR.png)

最后，审查通过就可以对拉取请求进行合并了，点击`Merge pull request`进行合并

![image-20210919005831430](https://i.loli.net/2021/09/19/K4EfVpQ1BvhwSFL.png)

点击`Confirm merge`，确认合并

![image-20210919005854745](https://i.loli.net/2021/09/19/ZYHrCAUJQvED93K.png)

合并成功之后，项目成员就可以看到修改的相关内容了

### 6.5、SSH 免密登录

1）基本语法

```bash
# -t指定加密算法，-C添加注释
ssh-keygen -t rsa -C 描述
```

2）案例实操

**本地生成 SSH 密钥**

键入命令，连敲三次回车即可

![image-20210919011352497](https://i.loli.net/2021/09/19/puY46lMsi2GkbKj.png)

进入`~/.ssh`目录，复制公钥信息

![image-20210919011953686](https://i.loli.net/2021/09/19/fZvNMLo1p7CGWIJ.png)

**GitHub 上添加公钥**

未添加任何公钥之前，`Code`—`SSH`会有警告提示信息，表示目前 SSH 方式是没有权限的

![image-20210919014241528](https://i.loli.net/2021/09/19/Zl6xeMd7qnV5UPW.png)

在 GitHub 的`settings`—`SSH and GPG keys`中，点击`New SSH key`添加一个公钥

![image-20210919012856831](https://i.loli.net/2021/09/19/pbSW2LukQAz5Cqj.png)

将`id_rsa.pub`即公钥信息粘贴至`Key`中，`Title`随意，点击`Add SSH key`进行添加

![image-20210919013103108](https://i.loli.net/2021/09/19/J1FOEVfW5bI6Tyl.png)

出现下列信息，说明添加成功

![image-20210919013731928](https://i.loli.net/2021/09/19/g1bZS56xRVdQIsm.png)

**验证 SSH免密登录 是否可用**

进入`git-demo`项目，点开`Code`—`SSH`，发现已经没有警告提示信息了，表示可用

![image-20210919014010529](https://i.loli.net/2021/09/19/DEvC6qPBAMS32ra.png)

复制 SSH 协议地址，使用`clone`命令克隆到本地，键入`yes`即可

![image-20210919015207022](https://i.loli.net/2021/09/19/Be8LsuUKFtbGf2j.png)

接下来就是修改内容、添加暂存区、提交本地库、推送远程库的操作了

这时候我们发现已经不再弹出登录授权的提示信息，就可以推送过去了

![image-20210919015907992](https://i.loli.net/2021/09/19/shjpkZWQNRwH9Gg.png)

查看远程库历史版本信息，确认推送成功

![image-20210919020511037](https://i.loli.net/2021/09/19/nla3Lbq2v5DWNcE.png)

至此，SSH 免密登录配置成功！



## 7、IDEA 集成 Git

### 7.1、配置 Git 忽略文件

问题1:为什么要忽略他们？答：与项目的实际功能无关，不参与服务器上部署运行。把它们忽略掉能够屏蔽 IDE 工具之间的差异。

问题2：怎么忽略？ 

**1）创建忽略规则文件 xxxx.ignore（前缀名随便起，建议是 git.ignore）**

这个文件的存放位置原则上在哪里都可以，为了便于让`~/.gitconfig`文件引用，建议也放在用户家目录下 

`git.ignore`文件模版内容

```properties
# Compiled class file 
*.class 
 
# Log file 
*.log 
 
# BlueJ files 
*.ctxt 
 
# Mobile Tools for Java (J2ME) 
.mtj.tmp/ 
 
# Package Files # 
*.jar 
*.war 
*.nar 
*.ear 
*.zip 
*.tar.gz 
*.rar 
 
# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml 
hs_err_pid* 
.classpath 
.project .settings target .idea 
*.iml 	crash 	logs,  	see 
```

**2）在 .gitconfig 文件中引用忽略配置文件（此文件在 Windows 的家目录中）**

```properties
[core]
	excludesfile = C:/Users/Archimedes/git.ignore
```

注意：这里要使用正斜线（`/`），不要使用反斜线（`\`）

### 7.2、定位 Git 程序

![image-20210919022336858](https://i.loli.net/2021/09/19/Ksamh3FIrUDgSQf.png)

### 7.3、初始化本地库

![image-20210919023500143](https://i.loli.net/2021/09/19/azTrXus8VPLlWUp.png)

明显看到，文件颜色变红了，代表着未被追踪。说明 Git 已经检测到 git-test 下文件，但是文件尚未被添加至暂存区

![image-20210919023714484](https://i.loli.net/2021/09/19/apHAoJ4l6qjvQc2.png)

### 7.4、添加至暂存区

![image-20210919023919818](https://i.loli.net/2021/09/19/Crp4b9lIw7TEfOD.png)

添加完毕之后，可以看到文件颜色变绿了，代表文件被追踪。说明 Git 已将文件添加至暂存区，但是尚未提交本地库

在`src`—`main`—`java`下创建一个`com.test.Test.java`文件

![image-20210919024327053](https://i.loli.net/2021/09/19/j2huey7ikESNRGK.png)

这是 IDEA 会自动检测到该文件，并提示是否需要将`Test.java`添加至暂存区

这里先`Cancel`，不直接`Add`单个文件，取而代之的是在整个项目上进行`Add`操作，这样整个项目下文件都可以被添加至暂存区

![image-20210919024618624](https://i.loli.net/2021/09/19/69TBRe8Jv4dLGNK.png)

这时会发现，`Test.java`文件变成绿色了，说明添加成功

![image-20210919024820302](https://i.loli.net/2021/09/19/Dt2mYwNhdnfpST8.png)

### 7.5、提交到本地库

![image-20210919025044021](https://i.loli.net/2021/09/19/Z7CVsT26SehXpNx.png)

点击`Commit Diretory...`之后，就可以看到暂存区的文件，输入日志信息就可以进行提交了

![image-20210919025135695](https://i.loli.net/2021/09/19/NlIThuxos4RSM87.png)

提交完毕之后，文件颜色也随之发生改变，说明 Git 已将文件提交至本地库

![image-20210919025455774](https://i.loli.net/2021/09/19/6p9ExHbcRLrXj8S.png)

### 7.6、切换版本

首先修改文件，观察到修改的文件颜色为蓝色，表示已修改状态，可以直接进行`commit`操作

![image-20210919025926937](https://i.loli.net/2021/09/19/6eSiHQO5AIwMkWE.png)

点击 IDEA 左下角 `Git`，可以查看历史版本

![image-20210919030209121](https://i.loli.net/2021/09/19/qxh3KQJHMWpD6Ew.png)

选定某一版本，点击`Checkout Reversion xxx`，可以进行版本穿梭

![image-20210919030832665](https://i.loli.net/2021/09/19/l7AMz5Z3kWGVPQy.png)

可以看到每次版本穿梭，`HEAD`指针的变化

![image-20210919031554124](https://i.loli.net/2021/09/19/62T7XWrRHtsxwaL.png)

![image-20210919031436323](https://i.loli.net/2021/09/19/rXSN8YjTEkPlF5M.png)

![image-20210919031358973](https://i.loli.net/2021/09/19/S3T7rIJuyb5jocm.png)

### 7.7、创建分支、切换分支

点击 IDEA 右下角`master`—`New Branch`就可以创建分支了

![image-20210919031946220](https://i.loli.net/2021/09/19/HnaCmTdoL4upSFW.png)

输入分支名，点击`Create`进行创建

![image-20210919032120261](https://i.loli.net/2021/09/19/r2vPU5a6iRuCnIm.png)

当然，也通过项目上`右键`—`Git`—`New Branch`，或者`右键`—`Git`—`Branches`—`New Branch`同理

![image-20210919032232261](https://i.loli.net/2021/09/19/U9KukNTEnG6PRMY.png)

切换分支同理，右键或是右下角均可

![image-20210919032658839](https://i.loli.net/2021/09/19/b5STdc2oFVwBMhQ.png)

### 7.8、合并分支

首先切换到`hot-fix`分支，修改内容后提交，再切换回`master`分支，同样在右下角选择我们需要合并的分支`hot-fix`，选择`Merge Selected into Current`，将`hot-fix`分支合并至`master`分支上

![image-20210919033803454](https://i.loli.net/2021/09/19/kU6VWa8FsE2YCwb.png)

发现内容已发生改变，并且查看历史版本也发生了变化

![image-20210919034137912](https://i.loli.net/2021/09/19/ovFEsWNSmcVtTwZ.png)

### 7.9、冲突合并

首先，分别切换`master`和`hot-fix`都对`Test.java`内容进行修改并提交

`master`版本信息

![image-20210919034805446](https://i.loli.net/2021/09/19/9F7WLDwgvzJusCx.png)

`hot-fix`版本信息

![image-20210919034838975](https://i.loli.net/2021/09/19/O6Go478iC3Wfvxr.png)

可以观察到，历史版本发生了分叉。现在将`hot-fix`合并至`master`上，提示`Conflicts`，说明合并出现了冲突

![image-20210919035044933](https://i.loli.net/2021/09/19/z2rZhe4PgfpOJBa.png)

点击`Merge`进行手动合并

![image-20210919035934596](https://i.loli.net/2021/09/19/BFxjaHqwE67rVhC.png)

解决完冲突后，会提示`All changes have been processed. Save changes and finish merging`，说明代码可以正常合并，点击`Apply`对手动合并的代码进行应用

![image-20210919040033465](https://i.loli.net/2021/09/19/Giq6AQa73OJFZ8w.png)

会发现文件颜色变为正常颜色，并且历史版本发生了改变，原来的两个分支合并成了一个

![image-20210919040319020](https://i.loli.net/2021/09/19/GaYv1BVDEgLnrAk.png)



## 8、IDEA 集成 GitHub

### 8.1、设置 GitHub 账号

**通过账号密码设置**

打开`Settings`，点击`Log In via GitHub...`

![image-20210919041647728](https://i.loli.net/2021/09/19/6bF8UzfwX3Nmx7W.png)

![image-20210919042210631](https://i.loli.net/2021/09/19/LZatlMudDzfAEYW.png)

会自动打开浏览器，进行授权确认

![image-20210919041726626](https://i.loli.net/2021/09/19/hAd8viWFMRVpuQI.png)

点击`Authorize in GitHub`后，会提示授权成功

![image-20210919041739608](https://i.loli.net/2021/09/19/Fleb53znrW7pkhI.png)

看到 IDEA 里新增了一条账号信息即为添加成功

![image-20210919041945459](https://i.loli.net/2021/09/19/QeuwdzBGcs7anNF.png)

**通过 Token 设置**

点击`Log In with Token...`

![image-20210919041312781](https://i.loli.net/2021/09/19/VGEAlaoq5WNH8Mx.png)

会弹出`Add GitHubh Account`框，输入我们在 GitHub 上创建的 Token 信息即可

![image-20210919042304290](https://i.loli.net/2021/09/19/di43r1mRlUDQguF.png)

如果还没有生成过或者丢失了之前创建的 Token，可以直接点击`Generate...`进行自动生成，默认已勾好权限

![image-20210919041530615](https://i.loli.net/2021/09/19/YZCbfpLdr2iqGRV.png)

修改并确认无误后，点击`Generate token`即可进行生成

![image-20210919042634756](https://i.loli.net/2021/09/19/PvoWfrhnH2VBYtQ.png)

Token 生成之后，只会在当前页面显示一次，需要及时复制保存下来

![image-20210919043209975](https://i.loli.net/2021/09/19/hf2gi1Nqr7QMwsI.png)

将 Token 粘贴至输入框，点击`Add Account`即可添加

![image-20210919043504031](https://i.loli.net/2021/09/19/gJiGtkPhxeCHEcN.png)

最后别忘了，一定要点击`Apply`和`OK`对设置进行保存

![image-20210919043630909](https://i.loli.net/2021/09/19/deXxBmpvEaLMhV7.png)

### 8.2、分享工程到 GitHub

我们一般会先在远程库创建一个`Repository`，再将本地库通过`remote`关联到远程库，最后进行版本推送

或者是先在远程库创建一个`Repository`，再通过`clone`将远程库克隆至本地，最后进行版本推送

而在 IDEA 中，可以将上述步骤合成一个步骤，即通过`Share`将本地库分享至 GitHub 上，非常便捷

![image-20210919044545203](https://i.loli.net/2021/09/19/AEwueUhD5f823cC.png)

填写完信息后，点击`Share`按钮，IDEA 会自动帮我们创建和初始化远程库，并将本地库推送至远程库

![image-20210919044648317](https://i.loli.net/2021/09/19/U6GEw1fVACkgI2a.png)

查看 GitHub 是否存在该仓库，以验证是否分享成功

![image-20210919045324286](https://i.loli.net/2021/09/19/zANscwaQLveHUXd.png)

在分享过程中，可能会出现如下报错：成功创建远程仓库，但是初始化推送失败。这时就需要进行手动`Push`的操作了

![image-20210919045442918](https://i.loli.net/2021/09/19/eHWxhpXrS6GtcIm.png)

### 8.3、Push 推送本地分支到远程库

![image-20210919045841143](https://i.loli.net/2021/09/19/BWsO5Qf7oKUwELM.png)

这里默认使用`https`协议进行推送，因为网络原因，很有可能推送失败

![image-20210919045959722](https://i.loli.net/2021/09/19/shLQSjTyRlMgxNW.png)

这是可以修改远程连接方式，点击`Define remote`设置新的远程别名

![image-20210919050127937](https://i.loli.net/2021/09/19/WFP6cxw7XsrNDEj.png)

然后会弹出一个重新定义远程方式的界面，这里使用 SSH 协议的远程地址即可（注意：不要与原来的别名重复）

![image-20210919050421674](https://i.loli.net/2021/09/19/7fXw3vpzuGDlHha.png)

点击`OK`后，可以重新选择远程别名，这里改为我们刚刚定义的 SSH 协议的别名：`origin-ssh`

![image-20210919050608057](https://i.loli.net/2021/09/19/EHqjVAe8gnUfiBT.png)

查看 GitHub 上历史版本修改内容，推送成功

![image-20210919050856473](https://i.loli.net/2021/09/19/Lw4n3yF2dlvVER9.png)

**注意**：`push`是将本地库代码推送到远程库，如果本地库代码跟远程库代码版本不一致， `push`的操作是会被拒绝的。也就是说，要想 `push`成功，一定要保证本地库的版本要比远程库的版本高！<mark>因此一个成熟的程序员在动手改本地代码之前，一定会先检查下远程库跟本地代码的区别！如果本地的代码版本已经落后，切记要先`pull`拉取一下远程库的代码，将本地代码更新到最新以后，然后再修改，提交，推送！</mark>

### 8.4、Pull 拉取远程库到本地

首先先修改远程库代码，然后进行如下操作

![image-20210919051622477](https://i.loli.net/2021/09/19/VxtYhksdG1M8Hc4.png)

选择 SSH 协议的别名，点击`Pull`进行代码拉取

![image-20210919051654972](https://i.loli.net/2021/09/19/9ZbGyQXSiOILcuf.png)

查看本地库代码易发生变化，并且历史版本也有了相关记录，说明代码拉取成功

![image-20210919051829325](https://i.loli.net/2021/09/19/D2eoI6qOYi1MKL7.png)

### 8.5、Clone 克隆远程库到本地

关闭项目，在 IDEA 选择页面，点击`Get From VCS`

![image-20210919134803024](https://i.loli.net/2021/09/19/mtbDjkgWrlOLF1G.png)

填写需要克隆的远程仓库地址和本地仓库地址，点击`Clone`进行克隆

![image-20210919135208275](https://i.loli.net/2021/09/19/6yLJFRQ5CaM7KDB.png)

等待克隆完成

![image-20210919135421271](https://i.loli.net/2021/09/19/7rpSQvmFXufk6aM.png)

初次进入项目，会提示是否信任并打开此 Maven 工程，一般选择`Trust Project`

如果勾选`Trust projects in xxx`，则在此工作空间下所有新增项目都将被信任，不会再提示

![image-20210919135528661](https://i.loli.net/2021/09/19/LPxn5sIySpJmoth.png)

打开项目，确认`Test.java`内容无误，历史版本记录正常

![image-20210919140005154](https://i.loli.net/2021/09/19/czytGlwKfYdbE2n.png)



## 9、国内代码托管中心**-**码云

众所周知，GitHub 服务器在国外，使用 GitHub 作为项目托管网站，如果网速不好的话，严重影响使用体验，甚至会出现登录不上的情况。针对这个情况，大家也可以使用国内的项目托管网站-码云

码云是开源中国推出的基于 Git 的代码托管服务中心，网址是 [https://gitee.com/](https://gitee.com/)，使用方式跟 GitHub 一样，而且它还是一个中文网站，如果你英文不是很好它是最好的选择



### 9.1、创建远程库

![image-20210919141130444](https://i.loli.net/2021/09/19/CpE3QtJ28brYSDq.png)

输入仓库名称，路径会自动与仓库名称保持一致，一般不改。选择开源，点击`创建`即可

![image-20210919141934714](https://i.loli.net/2021/09/19/Vp7BTjytOgMxbRK.png)

创建完毕会自动跳转到该项目界面，复制下列地址以备用

![image-20210919142145264](https://i.loli.net/2021/09/19/CULcZKBStwfe3sk.png)

### 9.2、删除远程库

打开项目`管理`—`仓库设置`—`删除仓库`，点击`删除仓库`

![image-20210919141337765](https://i.loli.net/2021/09/19/7CpdBi2K6Dq91ej.png)

输入确认信息，点击`确认删除`

![image-20210919141405164](https://i.loli.net/2021/09/19/fc6nN3FmAltUhq5.png)

输入密码，进行二次确认，点击`验证`，即可删除成功

![image-20210919141636996](https://i.loli.net/2021/09/19/4gSBl7K2LHdiprm.png)

### 9.3、IDEA 集成码云

首先安装 Gitee 的插件

![image-20210919142853337](https://i.loli.net/2021/09/19/8lw5kxBMr1WEC7N.png)

安装完成之后，点击`Apply`会刷新`Settings`选项，打开`Version Control`，多了一个`Gitee`选项

这里同样有两种方式，可以通过账号密码登录，也可以通过`Token`登录，操作同 IDEA 集成 `GitHub`

![image-20210919143042585](https://i.loli.net/2021/09/19/aLKo5PeuxrOYsZq.png)

输入完账号密码，点击`Log In`即可

![image-20210919143416998](https://i.loli.net/2021/09/19/9Ae24rVQhsdS8UX.png)

如果输入无误，便会在界面中展示账号信息，点击`OK`保存

![image-20210919143526220](https://i.loli.net/2021/09/19/UdGyi1nMHrBqjVX.png)

### 9.4、分享工程到 Gitee

![image-20210919143925298](https://i.loli.net/2021/09/19/CIGUkng89KJ1oqy.png)

如果远程仓库已存在该名称的项目，则会提示存在同名仓库无法删除，需要先删除刚刚我们创建的`git-test`仓库

![image-20210919144324387](https://i.loli.net/2021/09/19/PV4C9tensSI5y2M.png)

提示分享成功

![image-20210919144509857](https://i.loli.net/2021/09/19/DELbuOZay1rMUjF.png)

查看 Gitee，确认仓库创建成功并且推送成功

![image-20210919144634126](https://i.loli.net/2021/09/19/23YzcKHs7p5gjqf.png)

### 9.5、推送本地分支到远程库

修改内容，可以在左侧导航栏`Commit`直接进行提交并推送

![image-20210919145056974](https://i.loli.net/2021/09/19/pyMfPNUOxni7Sab.png)

同样可以自定义远程地址别名，点击`Push`进行推送

![image-20210919145252155](https://i.loli.net/2021/09/19/Ool6K3pZIFX2Nv7.png)

查看 Gitee 仓库历史版本记录，确认推送成功

![image-20210919145404382](https://i.loli.net/2021/09/19/AbYVFgop48wh5yK.png)

### 9.6、拉取远程库到本地

直接在 Gitee 上修改`Test.java`内容后，IDEA 中进行`Pull`即可

![image-20210919145655337](https://i.loli.net/2021/09/19/6L73UprJVqsYKdy.png)

选择我们指定的别名和分支，点击`Pull`进行拉取

![image-20210919145758217](https://i.loli.net/2021/09/19/sTcLU7rkj1IonVN.png)

查看`Test.java`即历史版本发生了变化，说明拉取成功

![image-20210919145913298](https://i.loli.net/2021/09/19/oAstIk7crm5PLhU.png)

### 9.7、克隆远程库到本地

![image-20210919150610990](https://i.loli.net/2021/09/19/BzLSQfd7knM1YoV.png)

### 9.8、码云复制 GitHub 项目

**导入仓库**

点击`从 GitHub / GitLab 导入仓库`

![image-20210919151012524](https://i.loli.net/2021/09/19/pmXHQloiZUvc7qb.png)

输入 GitHub 仓库地址，Gitee 会自动帮我们反填仓库名称及路径信息，修改为开源或私有，点击`导入`

![image-20210919151128894](https://i.loli.net/2021/09/19/lw2QKFcHdPAkOzi.png)

等待片刻

![image-20210919151354892](https://i.loli.net/2021/09/19/aWYpsSeR3QglUXH.png)

导入成功

![image-20210919151419992](https://i.loli.net/2021/09/19/3lqidkwohjvzYx5.png)

**强制同步**

如果后续该工程在 GitHub 上进行了修改，可以直接点击，刷新图标进行强制同步

![image-20210919151705859](https://i.loli.net/2021/09/19/fezXKLNMwgjUlHO.png)

需要注意的是强制更新会覆盖当前仓库，这里点击`确认`即可

![image-20210919151743598](https://i.loli.net/2021/09/19/GZfJnHwkd3gXa59.png)

查看历史版本记录，确认同步成功

![image-20210919151954815](https://i.loli.net/2021/09/19/aJmROA4rlniydLG.png)



## 10、自建代码托管平台 - GitLab

### 10.1、GitLab 简介

GitLab 是由 GitLabInc. 开发，使用 MIT 许可证的基于 网络的 Git 仓库管理工具，且具有 wiki 和 issue 跟踪功能。使用 Git 作为代码管理工具，并在此基础上搭建起来的 web 服务

GitLab 由乌克兰程序员 DmitriyZaporozhets 和 ValerySizov 开发，它使用 Ruby 语言写成。后来，一些部分用 Go 语言重写。截止 2018 年 5 月，该公司约有 290 名团队成员，以及 2000 多名开源贡献者。GitLab 被 IBM，Sony，JülichResearchCenter，NASA，Alibaba，Invincea，O’ReillyMedia，Leibniz-Rechenzentrum(LRZ)，CERN，SpaceX 等组织使用

### 10.2、GitLab 官网地址

- 官网地址：[https://about.gitlab.com/](https://about.gitlab.com/ ) 
- 安装说明：[https://about.gitlab.com/installation/](https://about.gitlab.com/installation/)

### 10.3、GitLab 安装

#### 服务器准备

准备一个系统为 CentOS7 以上版本的服务器，要求：内存 4G，磁盘 50G

关闭防火墙，并且配置好主机名和 IP，保证服务器可以上网

此教程使用虚拟机：主机名：`gitlab-server` IP 地址：`192.168.6.200`

#### 安装包准备

`Yum` 在线安装 `gitlab-ce` 时，需要下载几百 M 的安装文件，非常耗时，所以最好提前把所需 `RPM` 包下载到本地，然后使用离线 `rpm` 的方式安装

下载地址：

- [https://packages.gitlab.com/gitlab](https://packages.gitlab.com/gitlab)

注：资料里提供了此 `rpm` 包，直接将此包上传到服务器`/opt/module`目录下即可

####  编写安装脚本

安装 GitLab 步骤比较繁琐，因此我们可以参考官网编写 GitLab 的安装脚本

```bash
vim gitlab-install.sh
```

将下列脚本内容复制到创建的`gitlab-install.sh`文件中

```bash
sudo rpm -ivh /opt/module/gitlab-ce-13.10.2-ce.0.el7.x86_64.rpm
sudo yum install -y
curl policycoreutils-python openssh-server cronie
sudo lokkit -s http -s ssh
sudo yum install -y postfix
sudo service postfix start
sudo chkconfig postfix on
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
sudo EXTERNAL_URL="http://gitlab.example.com" yum -y install gitlab-ce
```

给脚本增加执行权限

```bash
chmod +x gitlab-install.sh
```

执行脚本变绿，说明具备执行权限

![image-20210919155804680](https://i.loli.net/2021/09/19/ulWb8f6YoVqmhir.png)

然后执行该脚本，开始安装 `gitlab-ce`。注意一定要保证服务器可以上网

```bash
./gitlab-install.sh
```

耐心等待片刻

![image-20210919160034134](https://i.loli.net/2021/09/19/dE87IpZ6meOYAhD.png)

脚本执行成功

![image-20210919160107808](https://i.loli.net/2021/09/19/xUEMp8hCQPsf6qK.png)

#### 初始化 GitLab 服务

执行以下命令初始化 GitLab 服务

```bash
gitlab-ctl reconfigure
```

过程大概需要几分钟，耐心等待…

![image-20210919160356614](https://i.loli.net/2021/09/19/oHXbw9vLy7Nfc3Y.png)

出现`gitlab Reconfigured!`说明 GitLab 服务初始化成功

#### 启动 GitLab 服务

执行以下命令启动 GitLab 服务

```bash
gitlab-ctl start
```

如需停止，执行

```bash
gitlab-ctl stop
```

服务启动成功

![image-20210919160530911](https://i.loli.net/2021/09/19/MhjB5uWJLCvqwze.png)

#### 使用浏览器访问 GitLab

使用主机名或者 IP 地址即可访问 GitLab 服务，使用主机名访问需要提前配置一下 windows 的 hosts 文件

![image-20210919160829896](https://i.loli.net/2021/09/19/JusPYkW5mxtX1Lf.png)

首次登陆之前，需要修改下 GitLab 提供的 root 账户的密码，要求 8 位以上，包含大小写子母和特殊符号。因此我们修改密码为 `Atguigu.123456`，然后使用修改后的密码登录 GitLab

![image-20210919161046164](https://i.loli.net/2021/09/19/O87nGbyHwSNR25x.png)

接下来，就可以用刚才修改的账号密码进行登录了

![image-20210919161237059](https://i.loli.net/2021/09/19/N4crZIPaSHqQYs3.png)

登录成功

![image-20210919161527493](https://i.loli.net/2021/09/19/QRMVNPos9p1huJy.png)

#### GitLab 创建远程库

我这里以官网 GitLab 为例，官网地址：[https://gitlab.com/](https://gitlab.com/)

官网还提供了 GitLab 自身的项目源码：[https://gitlab.com/gitlab-org/gitlab](https://gitlab.com/gitlab-org/gitlab)

![image-20210919163342358](https://i.loli.net/2021/09/19/DpyLwkR65obCqKG.png)

点击`New project/repository`—`Create a project`进行 GitLab 仓库的创建

![image-20210919163437259](https://i.loli.net/2021/09/19/VeFAgslZWUfSiY3.png)

填写项目信息后，点击`Create project`即可

![image-20210919163952615](https://i.loli.net/2021/09/19/Kne1cGhdZjSy6Do.png)

创建成功

![image-20210919164852273](https://i.loli.net/2021/09/19/vha8kXCZRr1nUdY.png)

#### IDEA 集成 GitLab

1）安装 GitLab 插件

![image-20210919162903737](https://i.loli.net/2021/09/19/OdNhaZrTb5GmlYy.png)

2）设置 GitLab 插件

![image-20210919173003661](https://i.loli.net/2021/09/19/QO2UeFrSkD5Pb6W.png)

出现相关信息，说明添加成功

![image-20210919173021265](https://i.loli.net/2021/09/19/vsa2qBHXLMNnb64.png)

3）push 本地代码到 GitLab 远程库

我们首先添加一个远程库别名

点击`Git`—`Manage Remotes`

![image-20210919165245464](https://i.loli.net/2021/09/19/vUoqfgdr9GuEKFw.png)

点击`+`号，自定义一个远程别名及对应远程库地址，点击`OK`

![](https://i.loli.net/2021/09/19/JGvlbNayTOujQom.png)

出现刚刚的记录，说明添加远程别名成功，点击`OK`

![image-20210919165610798](https://i.loli.net/2021/09/19/Gqh9P6nsQv7AWJS.png)

只要 GitLab 的远程库连接定义好以后，对 GitLab 远程库进行 pull 和 clone 的操作和 Github、码云一致，此处不再赘述
