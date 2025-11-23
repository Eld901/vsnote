# a6_02_DOC_Git  
`Created on 20240726 | Updated on 20240726`  
#### Git  
##### URL  
20240726 Git：https://www.bilibili.com/video/BV1HM411377j/  
##### vim 语法  
`vim file.xxx`  (进入 vim )  
`i`             (进入插入模式-- INSERT --)  
[Esc]           (退出插入模式)  
`:wq` [Enter]   (保存并退出 vim )  
`:q!`           (不保存强制退出 vim )  
`u`             (撤销)  
[Ctr+r]         (重做撤销)  
`/word`         (向下查找文本)  
`?word`         (向上查找文本)  
`:s/old/new/`   (替换当前行中的第一个 old 为 new)  
`:%s/old/new/g` (替换整个文件中的所有 old 为 new)  
##### 初始操作  
`git confit --global user.name "your name"`    (初始化命令)  
`git config --global user.email "your email"`  (初始化命令)  
`clear`  (清屏)  
##### 仓库操作  
`git clone <repository-url>`              (克隆仓库)`git clone https://github.com/user/project.git`  
`git status`                              (查看当前仓库的状态)  
`git remote add origin <repository-url>`  (添加一个新的远程仓库)`git remote add origin https://github.com/user/project.git`  
`git remote -v`                           (查看当前配置的远程仓库)  
`git pull origin <branch-name>`           (从远程仓库拉取最新的更改)  
`git push origin <branch-name>`           (将本地分支的更改推送到远程仓库)  
##### 分支操作  
`git branch <branch-name>`                (创建一个新的分支)  
`git checkout <branch-name>`              (切换到另一个分支)  
`git checkout -b <branch-name>`           (创建并切换到一个新分支)  
`git branch`                              (查看当前的分支)  
`git merge <branch-name>`                 (将一个分支的更改合并到当前分支)  
`git branch -d <branch-name>`             (删除一个分支)  
##### 文件操作  
`mkdir file`                  (新建文件夹)  
`git init file`               (初始化仓库)  
`git rm -r folder/`           (硬删除。有提示)  
`git rm --cached -r folder/`  (软删除。只保留本地，不保留暂存区)  
`touch file.xxx`              (新建文件。无内容)  
`echo "hhh" > file.xxx`       (新建文件。有内容)  
`git rm file.txt`             (硬删除。有提示)  
`git rm --cached file.txt`    (软删除。只保留本地，不保留暂存区)  
`cp -rf file1.xxx file2.xxx`  (将 file1.xxx 复制为 file2.xxx )  
`cat file.xxx`                (查看文件内容)  
`vim file.xxx`                (修改文件内容)  
`git diff file.xxx`           (对比修改前后)  
##### 提交操作  
`git add .`                         (将文件添加到暂存区)  
`git add file.xxx`                  (将文件添加到暂存区)  
`git reset --soft`                  (撤销提交。保留工作区，保留暂存区)  
`git reset --mixed file.xxx`        (撤销提交。保留工作区，丢弃暂存区)`git reset file.xxx`  
`git reset --hard file.xxx`         (撤销提交。丢弃工作区，丢弃暂存区)  
`git reset --soft HEAD~1`           (撤销最近一次提交。保留工作区，保留暂存区)  
`git reset --mixed HEAD~1`          (撤销最近一次提交。保留工作区，丢弃暂存区)  
`git reset --hard HEAD~1`           (撤销最近一次提交。丢弃工作区，丢弃暂存区)  
`git restore --staged file.xxx`     (取消暂存，保留工作区)  
`git restore file.xxx`              (取消暂存，丢弃工作区)`git checkout -- file.xxx`  
`git commit file.xxx -m "message"`  (提交到仓库)  
`git commit -am "message"`          (提交暂存和仓库)  
`git status -s`                     (查看提交状态)  
##### 查看操作  
`git diff <file>`             (查看文件的更改)  
`git diff --staged`           (查看暂存区的更改)  
`git reflog`                  (查看引用日志。恢复丢失的提交)`git reset --hard HEAD@{1}`  
`git log --oneline`           (查看历史提交列表)  
`ls`                          (Linux)  
`git ls-files`                (列出所有被跟踪的文件)  
`git ls-files --cached`       (列出暂存区中的文件)  
`git ls-files --deleted`      (列出已删除但尚未提交的文件)  
`git ls-files --modified`     (列出已修改但尚未暂存的文件)  
`git ls-files --others`       (列出未跟踪的文件，不包括 .gitignore)  
`git ls-files --ignored`      (列出被 .gitignore 忽略的文件)  
`git ls-files --stage`        (显示文件的暂存区信息)  
##### 其他操作  
`git tag <tag-name>`          (创建一个标签)  
`git tag`                     (查看所有标签)  
`git push origin <tag-name>`  (推送标签到远程仓库)  
`git help <command>`          (查看 Git 命令的帮助文档)  
##### 忽略跟踪  
.gitignore  用于指定文件或目录不被纳入版本控制  
1. 基本规则  
空文件夹默认不会被纳入版本控制  
已提交到仓库的文件会被纳入版本控制  
2. 语法规则  
注释：`#`  
任意：`*`  
单个：`?`  
任选：`[]`  
取反：`!`  
范围：`[0-9]` `a-z` `A-Z`  
2. 基本用法  
忽略单文件：`file.txt`  (文件名)  
忽略多文件：`*.log`  (*.后缀名)  
忽略文件夹：`file/`  (文件名/)  
3. 常用示例  
`*.log`  忽略所有`.log`文件  
`!file.txt`  忽略所有`.txt`文件除了`file.txt`文件  
`file/*.txt`  忽略`file`文件夹下的`.txt`文件，不包括子目录  
`file/**/*.txt`  忽略`file`文件夹下的`.txt`文件，包括子目录  
`file/`  忽略任何目录下的`file`文件夹  
`/file`  忽略当前目录下的`file`文件夹，不包括子目录  
##### 小结 rm  
###### (0)前置  
分别执行删除命令、git status的返回提示  
###### (1)普通删除：仓库删除，暂存区删除，本地删除，无提示  
```git 
<!-- rm file.txt -->
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    1.txt
```
###### (1)硬删除：仓库删除，暂存区删除，本地删除，有提示  
```git
<!-- git rm file.txt -->
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    1.txt
```
###### (1)软删除：仓库删除，暂存区删除，本地保留  
```git
<!-- git rm --cached file.txt -->
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1.txt
```
##### 小结 reset  
###### (0)新建三个commit操作  
```git
<!-- 步骤1：新建gitest文件夹，新建txt文件-->
$ cd gitest
$ touch 1.txt 2.txt 3.txt

<!-- 步骤2：提交操作-->
$ git add .
$ git commit 1.txt -m "1.txt"
$ git commit 2.txt -m "2.txt"
$ git commit 3.txt -m "3.txt"

<!-- 步骤3：复制gitest为t1、t2、t3文件夹-->
$ cd ..
$ cp -rf gitest t1
$ cp -rf gitest t2
$ cp -rf gitest t3
```
###### (1)soft 保留工作区，保留暂存区  
```git
<!-- soft-->
$ cd t1
$ git reset --soft HEAD^

<!-- 工作区：保留-->
$ ls
1.txt  2.txt  3.txt

<!-- 暂存区：保留-->
$ git ls-files
1.txt
2.txt
3.txt

<!-- 提示(新文件，添加到暂存区，未提交到仓库)-->
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   3.txt
```
###### (2)mixed 保留工作区，丢弃暂存区  
```git
<!-- mixed-->
$ cd t3
$ git reset --mixed HEAD^

<!-- 工作区：保留-->
$ ls
1.txt  2.txt  3.txt

<!-- 暂存区：丢弃-->
$ git ls-files
1.txt
2.txt

<!-- 提示(新文件，未添加到暂存区)-->
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        3.txt
```
###### (3)hard 丢弃工作区，丢弃暂存区  
```git
<!-- hard-->
$ cd t2
$ git reset --hard HEAD^

<!-- 工作区：丢弃-->
$ ls
1.txt  2.txt

<!-- 暂存区：丢弃-->
$ git ls-files
1.txt
2.txt

<!-- 提示(已在仓库)-->
On branch master
nothing to commit, working tree clean
```
###### (4)返回消息  
`Untracked files`                         (新文件，未添加到暂存区)  
`Changes to be committed`                 (新文件，添加到暂存区，未提交到仓库)  
`modified`                                (已在暂存区，修改文件内容，未提交到仓库)  
`deleted`                                 (已在暂存区，删除文件，未提交到仓库)  
`nothing to commit, working tree clean`   (已在仓库)  
##### 08 github、gitee、gitlab私有化部署  
【Ctrl+Insert】复制  【Shift+Insert】粘贴  
`git clone` `git add .` `git commit -m commit` `git push`  
1. 克隆github仓库到本地  
`git clone <github repository path>`  
2. 添加新的远程仓库gitlab  
`git remote add <repository alias> <gitlab repository path>`  
3. 移除远程仓库  
`git remote remove <repository alias>`  
4. 查看远程仓库地址  
`git remote -v`  
5. 提交本地仓库到github默认仓库  
`git push`  
6. 提交本地仓库到新的远程仓库  
`git push <repository alias> main`  

