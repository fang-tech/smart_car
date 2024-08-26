# Git 

## 版本控制系统

- Git 是当前最先进的分布式管理系统
- 分布式对比集中式管理的优势
  - 集中式只有一个单一的中央仓库, 开发者需要持续联网, 修改仓库中的代码, 仓库炸了, 就完了
  - 分布式在每个开发者的本地都有完整的本地仓库副本, 只需要在同步的时候上传

## 用户的创建

- 创建用户名

  - ```bash
    git config --global user.name "Fun T"
    ```

  - (Local) 省略: , 本地配置, 只对本地的仓库有效

  - --global : 全局配置, 对所有仓库有效
  - --system : 系统配置, 对所有的用户有效

- 创建邮箱

  - ```bash
    git config --global user.email tianyufang978@gmail.com
    ```

- 保存配置

  - ```bash
    git config --global credential.helper store
    ```

- 查看配置信息

  - ```bash
    git config --global --list
    ```

## 新建版本库

- 创建仓库

  - 直接初始化本地文件夹, 先进入到这个文件夹中

    - ```bash
      git init 仓库名(可选)
      ```

  - 从clone GitHub上现有的仓库

    - ```bash
      git clone 仓库的URL
      ```

##  工作区域和文件状态

- 工作区域分为三种

  - 工作区
  - 暂存区
  - 本地仓库

- 说明

  - 工作区就像是整个房间, 你可以自由地在这里添加, 移动, 修改或删除物品. 这是日常工作的地方, 所有的改动都发生在这里

  - 暂存区, 可以想象成一个房间中的大房子. 当你决定要保存哪些改动的时候, 你可以将这些改动放进箱子中, 这是一个中间步骤, 用于让你思考, 哪些改动是需要保存的

  - 本地仓库 : 这就像是你的相册或日记, 当你确定要永久保存箱子里的物品的时候, 你会拍下一张照片或在日记中记录下来, 这里储存了你项目的所有历史版本(储存在`.git/objects`)

- 文件状态

  - Untracked (未跟踪的) : 

    - 想象这些是图书馆外面的新书, 还没有登记入库, Git知道他们的存在, 但不会主动关注他们的变化
    - 一般是新创建的文件或者从`.gitignore`中的移除的文件
    - 我们可以使用`git add`将它们"登记入库"

  - Staged (暂存) :

    - 这就像是图书管理员的工作推车, 书已经从外面拿进来了, 正在决定哪些书籍需要上架
    - 是在使用`git add`添加Untracked或者Modified文件后
    - 使用`git commit`将变更永久保存, 或`git  reset`将文件从暂存区中移除

  - Modified (已修改) : 

    - 想象有人接走了一本书, 在上面做了笔记后归还. 内容已经改变, 但还没有正式更新到图书馆的记录中
    - 编辑Unmodified状态的文件到达该状态
    - 使用git add将变动存入暂存区, 或git checkout放弃更改

  - Delete(已删除) : 

    - 这就像是准备将某本书下架, 但还没有在图书馆的系统中更新这个信息
    - 使用`git rm`或者直接删除了某个文件, 会达到该状态
    - 使用`git add`确认删除操作, 或`git checkout`恢复文件

  - Copied (已复制) :

    - 就像图书馆制作了一本书的副本, 但是还没有正式编入目录
    - 使用特定的Git命令复制文件(不常见), 会达到该状态
    - 使用`git add`确认复制操作

  - Renamed (已重命名) : 

    - 相当于换了一个书名, 但还没有更新图书馆的目录

    - 使用`git mv`重命名文件, 或者是直接在文件系统中重命名文件
    - 使用`git add`确认重命操作

  - Updated but Unmerged  (更新但未合并) :

    - 想象两个图书管理员同时修改了同一本书的不同部分, 现在需要决定如何将这些改动合并成一个版本
    - 在合并和rebase操作中遇到冲突
    - 手动解决冲突, 然后使用`git add`标记为已解决

- 表格说明, 工作区域与文件状态变化

| 文件状态                  | 原始位置       |   执行命令   | 新位置                            |
| ------------------------- | -------------- | :----------: | --------------------------------- |
| Untracked                 | 工作区         |   git add    | 暂存区                            |
| Modified                  | 工作区         |   git add    | 暂存区                            |
| Staged                    | 暂存区         |  git commit  | 本地仓库                          |
| Unmodified                | 本地仓库       |   文件修改   | 工作区（变为Modified）            |
| Deleted（从文件系统删除） | 工作区         |   git add    | 暂存区                            |
| Deleted（使用git rm）     | 工作区和暂存区 |  git commit  | 本地仓库                          |
| Renamed（使用git mv）     | 工作区和暂存区 |  git commit  | 本地仓库                          |
| Staged                    | 暂存区         |  git reset   | 工作区（变为Modified或Untracked） |
| Modified                  | 工作区         | git checkout | 与本地仓库同步（变为Unmodified）  |

## 添加和提交文件

- 添加文件

  - ```bash
    git add
    ```

  - 也可以使用通配符`git add *.txt`

  - 也可以使用目录`git add .`

- 提交文件

  - ```bash
    git commit -m "提交信息" 
    ```

  - 只提交暂存区中的内容, 不会提交工作区中的内容

-  查看仓库状态

  - ```bash
    git status
    ```

- 查看仓库提交历史记录

  - ```bash
    git log --oneline(可选, 用于查看简介的提交记录)
    ```




## 回退版本

- 基础命令

  - ```bash
    git reset --模式
    ```

- 三种模式

  - --soft
    - 保留原先的工作区和暂存区的内容
  - --hard
    - 清空原先的工作区和暂存区的内容
  - --mixed
    - 保留工作区的内容和, 但是删除暂存区的内容

## 查看差异

- 基础命令

  - ```bash
    git diff
    ```

  - 默认比较的是工作区和暂存区的内容

- 比较工作区和版本库之间的差异

  - ```bash
    git diff HEAD
    ```

- 比较暂存区和版本库之间的差异

  - ```bash
    git diff --cached
    ```

- 比较两个特定版本之间的差异

  - ```bash
    git diff ID_1 ID_2
    ```

- 比较当前版本和现在版本之间的差异

  - ```bash
    git diff HEAD~ HEAD
    ```

- 只比较特定文件内容之间的差异

  - ```bash
    git diff HEAD~3 HEAD file3.txt
    ```

  - 比较当前版本和当前版本的前三个版本之间的file3.txt之间的差异

## 删除文件

- 查看暂存区中的文件列表

  - ```bash
    git ls-files
    ```

- 删除文件

  - 直接在文件操作系统中, 然后再`git add .`

  - 使用Git的命令, 将文件同时从工作区和暂存区中删除

  - 把文件同时从暂存区和工作区删除

    - ```bash
      git rm <file> 
      ```

  - 把文件从暂存区中删除, 但是工作区中的内容还保留

    - ```bash
      git rm --cached <file>
      ```

  - 递归删除某个目录下的所有子目录和文件, 删除后不要提交

## gitignore

- 忽略的策略

  - 忽略中间文件, 也就是由另一个文件自动生成的文件, 比如C语言的.exe文件
  - 忽略敏感配置文件

- 添加需要忽略的文件

  - ```bash
    <file> -> 忽略某个特定的文件
    ```

  - ```bash
    folder/ -> 忽略指定的文件夹
    ```

  - ```bash
    *.exe -> 忽略后缀为.exe的文件
    ```

- 匹配规则

  - 空行和以#开头的行会被Git忽略. 一般空行用于可读性的分隔, # 一般用于注释
  - 标准的Blob模式匹配
    - 星号 * 通配任意个字符
    - 问好 ? 匹配单个字符
    - 中括号[]表示匹配列表中的单个字符, 比如: [abc] 表示a/b/c
  - 两个星号 ** 表示匹配任意的中间目录
  - 中括号可以使用短中线连接, 比如:
    - [0-9]表示任意一位数字, [a-z]表示任意一位小写字母
  - 感叹号 ! 表示取反 (强制保留) 


## 远程连接Github仓库

- 身份验证

  - 使用Git连接远程仓库通常需要验证身份, 以确保只有授权用户才能访问和修改代码, 以下是常见的身份验证方式

    - 用户名和密码验证 (已淘汰)
    - SSH密钥 : 更安全和方便的方法, 也是目前的标准做法, 只需要设置一次即可
    -  个人访问令牌(PAT) : 广泛用于AP和命令行操作

  - 设置SSH密钥

    - ```bash
      # 生成新的SSH密钥对
      ssh-keygen -t ed25519 -C "your_email@example.com"
      
      # 如果你使用的是不支持Ed25519算法的旧系统, 使用 : 
      # ssh-keygen -t rsa 4096 -C"your_email@example.com"
      
      # 接下来的两个步骤可以省略, 但建议还是运行
      # 启动ssh-agent
      eval "$(ssh-agent -s)"
      
      # 将SSH私钥添加到ssh-agent
      ssh-add ~/.ssh/id_ed25519
      
      # 复制公钥的内容到剪切板
      cat ~/.ssh/id_ed25519.pub | clip
      
      ```

- 在Github设置SSH

  -  在用户找到SSH and GPG keys
  - 添加SSH 密钥, 并将公钥的内容复制过去
  - 保存

- 克隆仓库

  - ```bash
    git clone repo-address
    ```

- 推送更新内容

  - ```bash
    git push <remote><branch>
    ```

- 拉取更新内容

  - ```bash
    git pull <remote>
    ```

## 关联本地仓库和远程仓库

- 添加远程仓库

  - ```bash
    git remote add <远程仓库名> <远程仓库地址>
    ```

- 将本地仓库的内容推送到远程仓库

  - ```bash
    git push -u <远程仓库名> <分支名>
    ```

- 查看远程仓库

  - ```bash
    git remote -v
    ```

- 拉取远程仓库内容

  - ```bash
    git pull <远程仓库名> <远程分支名>:<本地分支名>
    git fetch <远程仓库名> <远程分支名>:<本地分支名>
    # 远程分支名和本地分支名相同则省略冒号后面的部分
    ```

  - 区别 : 
    - pull会自动执行合并操作
    - fecth需要手动合并

## 分支

- 出现情景 : 
  - 多人协同同时开发一个项目, 即可每个人创建一个新的分支用于完成自己的工作内容, 完成以后, 再将自己的修改内容推送到主分支上, 这样能保证主分支始终是可运行的

- 查看分支列表

  - ```bash
    git branch
    ```

-  创建分支

  - ```bash
    git branch <branch-name>
    ```

- 切换分支

  - ```bash
    git switch <branch-name>
    ```

- 合并分支

  - ```bash
    git merge branch-name
    ```

- 删除分支

  - ```bash
    git branch -d branch-name # 已合并
    ```

  - ```bash
    git branch -D branch-name # 未合并, 强制删除
    ```

##  解决合并冲突

- 出现情景 : 

  - 两个分支同时修改了同一个文件的代码, 这个时候git就不知道该保留哪一个分支的修改内容

- 处理冲突的流程

  - 问题背景 : 

    - 在branch-main 修改了file.txt文件的内容, 并add and commit

    - 在branch-feat 修改了file.txt文件的内容, 并add and commit

    - 在branch-main 

      - ```bash
        git merge feat
        ```

  - 解决流程

    - `git status`用于查看哪些文件出现了冲突
    - `git diff`用于查看详细的冲突内容
    - 使用vim或者别的编辑器手动解决冲突
    - `git add  ` and `git commit`
    - 也可以放弃合并`git merge abort`

- 特殊问题

  - 将txt文件识别为二进制文件(binary file)

    - 问题类型 : 

  - 解决方法(一) : 修改文件格式

    - 检查文件的格式

    - ```bash
      file <file-name>
      ```

    - 确保输出的是git支持的文件编码格式 : UTF-8, GBK等

    - 如果不是则需要修改文件编码格式为支持的编码格式

  - 解决方法(二) : 添加配置文件.gitattributes

    -  添加下列内容, 即可diff

    - ```
      *.txt                                          diff
      *.txt	text
      ```

    - 设置git将.txt 视作文本文件, 并且用常规文件比较方式比较

## rebase

- 目的

  - 重写项目的提交历史, 也就是commit的历史

- 使用

  - 位置为branch-main, 在此之前, 两个分支经历过合并

  - ```bash
    git rebase dev
    ```

  - 将main的提交历史变基到dev提交历史后面


## cherry-pick

- 简要说明

  - 将特定的提交从一个分支复制到另一个分支, 这个命令的名字很形象 - 就像在樱桃树上精选最好的樱桃一样,你可以从一个分支上"摘取"你想要的特定提交。

- 主要用途

  1. 将特定的功能或修复应用到多个分支
  2. 从废弃的分支中salvage work
  3. 回滚特定的更改
  4. 在不合并整个分支的情况下应用特定更改

- 基本语法

  - ```bash
    git cherry-pick <commit-hash>
    ```

  - ```bash
    master:  A---B---C---D
                    \
    feature:          E---F---G
    ```

  - 执行cherry-pick后，分支结构会变成这样：

  - ```bash
    master:  A---B---C---D---F'
                    \
    feature:          E---F---G
    ```

  
  ## rabase 与 merge
  
  ![merge和rebase对比图](../res/images/image1.png)
  
  - rebase可以整理 









