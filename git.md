# 基本操作

## git创建一个版本库

1. 新建一个目录git_test, 在git_test目录下创建一个版本库：

   > 1. `mkdir git_test`
   >
   > 2. `cd git_test`
   > 3. `git init`  初始化后git可管理此目录下的所有文件

## 使用

1. git add `file_name` 

   > 添加文件file_name

2. git commit -m `'说明信息'`

   > `git commit` 创建版本
   >
   > `-m` 后有空格， 单引号内写说明信息

3. 使用`git log` 查看版本记录

4. 对`file_name` 修改后，执行1 2 3 步，可看到有两个创建信息

5. 若想回到之前某一个版本，可以使用`git reset --hard HEAD^ ` 

   > - 其中`HEAD` 表示当前最新版本，`HEAD^` 表示当前版本的前一个版本，`HEAD^^` 表示当前版本的前两个版本
   > - 也可以使用`HEAD~1` 表示当前版本的前一个版本，`HEAD~100` 表示当前版本的前100个版本

6. 若想回到之后的某个版本，可以使用`git reset --hard 版本号` 

   > 版本号即为`git log ` 结果中 commit 之后的数字串， 可以不全部拷贝，只拷贝前几位

7. `git reflog` 可以查看操作记录，结果中的前面数字串为版本序列号

## 工作区和暂缓区

1. 工作区

   > 电脑中的目录，比如git_test, 就是一个工作区。

2. 版本库

   > 工作区有一个隐藏目录`.git` (使用`ls -al`可查看)， 这个不是工作区，而是git的版本库。
   >
   > git的版本库里存了很多东西，其中最重要的就是被称为stage（或者index）的暂存区，还有git为我们创建的第一个分支，和指向master的一个指针叫HEAD

   > 把文件往git版本库里添加的时候，分两步执行：
   >
   > - `git add` 把文件修改添加到暂存区
   > - `git commit`   一次性把暂存区的所有内容提交到当前分支

> `git status` 查看当前工作树的状态

3. 管理修改

   > git管理文件的修改，**它只会提交暂存区的修改并创建版本**

4. 撤销修改

   > - 使用`git checkout -- file_name` 撤销**未加入**暂存区里的修改
   >
   > - 使用`git reset HEAD file_name` 把暂存区里的撤销掉，重新放回工作区

5. 对比文件不同

   > 对比工作区和版本库某个文件 `git diff HEAD -- file_name`
   >
   > `git diff HEAD HEAD^ -- file_name`
   >
   > `git diff HEAD^ HEAD -- file_name`
   >
   > - 结果中 -- 代表 HEAD版本
   > - ++ 代表 HEAD＾版本

6. 删除文件

   > 编辑、创建、删除文件都是对工作区的改动
   >
   > - 删除本地文件 `rm file_name`
   > - 撤销删除 `git checkout -- file_name` 此时文件恢复到本地
   > - `git rm file_name`  将删除添加到暂存区
   > - 若想将暂存区删除撤销，同4.
   > - 若确定删除，则`git commit`

> 若版本记录过长，可以简短形式显示 `git log --pretty=oneline`

# 分支管理

## 创建与分支合并

1. 查看当前分支个数且在哪个分支工作

   > `git branch` 

2. 创建并切换分支

   > - `git branch dev` 创建新分支dev
   >
   > - `git checkout -b dev` 创建并切换到新分支dev
   >
   > - `git checkout master` 切换到分支master

3. 合并分支

   > `git merge dev` **快速合并**dev到master

4. 删除分支

   > `git branch -d dev` 删除分支dev

## 解决冲突

两个分支都提交后不能使用快速合并，此时会发生冲突。

可将冲突文件重新修改再提交解决冲突。

> `git log --graph --pretty=oneline` 查看冲突解决过程

## 分支管理策略

> - 分支冲突
>
>   > 两个分支都有了新的提交记录并且修改的是同一个文件
>
> - 管理策略
>
>   > - 合并的时候，如果可以，执行快速合并，但会损失分支提交记录
>   > - 禁止快速合并`git merge --no-ff dev`

## bug分支

> - `git stash` 保存工作现场
> - 切换到bug所在分支，创建并切换到一个临时分支，修复bug
> - 修复完bug之后，切换回bug所在分支，使用no-ff模式合并分支，删除临时分支
> - 切换回工作分支，`git stash pop` 恢复工作现场

# github

> `git init` 初始化本地文件夹
>
> `git remote add origin 仓库https/ssh` 将本地文件夹与远程仓库链接
>
> `git push origin branch_name` 推送到远程分支
>
> `git branch -m branch_name` 更改当前分支名字
>
> `git branch --set-upstream-to=origin/origin_branch local_branch` 将本地分支跟踪远程分支
