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
