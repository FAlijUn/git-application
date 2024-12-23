## 已提交 修改了文件，但是没有保存到数据库
## 已修改 数据已经安全的保存在本地文件
## 已暂存 对于当前版本进行了标记，

## 工作目录 对于项目的某个版本提取的内容
## 暂存区域 保存了下次要提交的文件列表信息
## git仓库 保存项目元数据

## 工作流程 在工作区域修改文件，将提交选择性地暂存，提交更新找到暂存区的文件，将快照保存在git目录


## 命令行指令列表

### 安装基本的git工具 sudo apt install git-all

### 运行git的配置
    查看所有配置 git config --list
    查看所有配置已经配置所在的文件夹 git config --list  --show-origin
    设置git的用户名字 git config --global user.name "xxx"
    设置git的用户邮箱 git config --globel user.email "xxx@example.com"
    --global,git 都会用到相应的信息
    对于特定的项目使用不同的用户信息, 运行没有--global的配置
    可以通过 git config <key> 来检查某一项配置

### 获取帮助
  git help <config>
  git <config> --help / -h 不是全面的手册
  man git-help

### 初始化工作目录 git init 该命令将创建一个.git的子目录
    ```
      git add *.c
      git add LICENSE
      git commit -m 'initial project version'
    ```
    git clone <url> 克隆一个仓库

### 记录每次更新到仓库
    已跟踪和未跟踪
    git add 将没有被追踪的文件转换成被追踪的文件

### 忽略文件 有一些文件无需纳入git的管理，创建一个.gitignore
### .gitignore 的文件规范
      所有空格或者#开头的行会被忽略(相当与注释)
      glob模式匹配，(*)匹配0个或者多个字符,[abc]匹配在[]中任何一个字符,[0-9]，匹配0到9数字的一个，(**)匹配任意中间目录a/**/z
      匹配模式以/开头防止递归
      匹配模式以/结尾指定目录
      ！取反
      ```
        # 忽略所有的 .a 文件
        *.a

        # 但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
        !lib.a

        # 只忽略当前目录下的 TODO 文件，而不忽略 subdir/TODO
        /TODO

        # 忽略任何目录下名为 build 的文件夹
        build/

        # 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
        doc/*.txt

        # 忽略 doc/ 目录及其所有子目录下的 .pdf 文件
        doc/**/*.pdf
      ```

### 想知道具体修改了什么地方 git diff
### 查看已暂存将要添加到下一次提交里的内容 git diff --staged

### 先用 git status 看下，你所需要的文件是不是都已暂存起来了， 然后再运行提交命令 git commit
  git commit -m ""
  git commit -a -m "" 跳过git add

### 移除文件
  在工作目录下 rm之后再运行git rm
  具体来说，它会从 Git 的索引（即暂存区）中移除文件，使得 Git 不再跟踪该文件，但文件仍然存在于你的本地文件系统中

### 移动文件
  git mv file_from file_to 相当于重命名文件

### 查看提交历史
  git log
  git log -p 显示每次提交所引入的差异（按 补丁 的格式输出）
  git log --stat
  git log --pretty=oneline
  git log --pretty=format:"%h %s" --graph 展示分支和和并历史

### 撤销操作
  git commit --amend
  git reset HEAD <file name> 取消暂存
  git checkout -- CONTRIBUTING.md 撤销对文件的修改

### 远程仓库的使用
  git remote 查看远程仓库
  git remote add <shortname><url> 添加一个新的远程仓库
  git fetch <origin> 从远程仓库中获取数据
  git push  <origin> <branch> 推送到远程仓库
  git remote show origin
  git remote rename <shortname> <other_shortname>
  git remote remove <shortname> 移除一个远程仓库

### 标签
  git tag <v0.1> 轻量标签
  git tag -a <v0.1> -m "xxxx" 附注标签  
  git push origin <tagname> 创建完标签显示的推送
  git push origin :refs/tags/v0.1 | git push origin --delete <tagname> 删除标签 
  git checkout -b <branch_name> <tag_name>

### 别名
  ```
  git config --global alias.co checkout
  git config --global alias.br branch
  git config --global alias.ci commit
  git config --global alias.st status
  ```

### 分支 git分支包含5个对象 3个blob对象(保存文件快照)，1个树对象(目录结构和blob对象索引)，1个提交对象树对象指针和所有提交信息
  git branch <branchname> 创建一个分支
  HEAD指针指向当前所在的本地分支
  git checkout <branchname> 切换到新创建的分支
  git checkout -b <branchname> 创建新的分支同时切换过去
  git merge <branchname> 合并回主线
  git branch -d <brachname> 删除分支
  合并冲突 查看冲突文件： 打开有冲突的文件，Git 会在冲突的地方插入冲突标记（通常是 <<<<<<<, =======, >>>>>>>），让你看到不同分支之间的差异
  git branch --merged 已经合并的分支
  git branch --no-merged 还没有合并的分支

### 分支开发工作流
  master 保留完全稳定 已经发布或者即将发布的分支
  develop/next 开发测试分支，分支不必保持绝对稳定，但是一旦达到稳定状态，它们就可以被合并入 master 分支

### 远程分支
  git ls-remote <origin> 远程引用的完整列表
  git branch -u origin/<branch>
  git push origin --delete <branch> 删除远程分支

### 变基 merge rebase
  git rebase <branchname> 将提交到某一个分支的所有修改都移到另一个分支上
  git rebase --onto master server client 取出 client 分支，找出它从 server 分支分歧之后的补丁， 然后把这些补丁在 master 分支上重放一遍，让 client 看起来像直接基于 master 修改一样
  git pull --rebase

### 服务器上的git
  本地协议(Local protocol) 其中的远程版本库就是同一主机上的另一个目录 git remote add <远程仓库名> <url>

### 其他工具
  git log --abbrev-commit --pretty=oneline
  git show
  git rev-parse <branchname>
  git reflog 引用日志
  git show HEAD^ 查看上一个提交
  git stash push
  git stash list
  git stash apply 将刚刚贮存的进行应用
  git clean -f -d 移除工作目录中没有被追踪到的文件以及空的子目录

### 签署
  gpg --gen-key 生成一个密钥
  git config --global user.signingkey 0A46826A 密钥签署提交

### 搜索
  git grep

### 重写历史
  git filter-branch --tree-filter 'rm -f xxx.txt' HEAD 全局修改你的邮箱地址或从每一个提交中移除一个文件
  --tree-filter 选项在检出项目的每一个提交后运行指定的命令然后重新提交结果
  全局修改邮箱地址
  ```
    git filter-branch --commit-filter '
        if [ "$GIT_AUTHOR_EMAIL" = "schacon@localhost" ];
        then
                GIT_AUTHOR_NAME="Scott Chacon";
                GIT_AUTHOR_EMAIL="schacon@example.com";
                git commit-tree "$@";
        else
                git commit-tree "$@";
        fi' HEAD
  ```

### 重置
  git reset <key> 移动 HEAD的指向
  git commit --amend

## 合并冲突
  git checkout --conflict=diff3 hello.rb

  git reset --hard HEAD 回到上一次提交的状态
  git merge -Xignore-space-change whitespace 忽略空白的修改
  git revert -m 1 HEAD 撤销合并提交 如果你要撤销一个合并提交，可以使用 -m 选项指定合并提交的父提交
  git revert 命令用于撤销某次提交的更改，并创建一个新的提交来“反做”原有提交的更改