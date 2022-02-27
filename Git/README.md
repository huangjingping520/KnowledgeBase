# Git

### Git 与 SVN 的区别

Git是**分布式**版本控制系统，没有中央服务器。

SVN是**集中式**版本控制系统，版本库是集中放在中央服务器的。


### Git基本理论

> 工作区域

Git本地有三个工作区域： 

- 工作目录(Working Directory)
- 暂存区(Stage/Index)
- 资源库(Repository/Git Directory)

如果加上远程的git仓库(Remote Directory)就可以分为四个工作区域。

> 关系

![](https://gitee.com/merlinalex/pic-go/raw/master/20220227221212.png)

> 工作流程

1. 在工作目录中添加、修改文件
2. 将需要进行版本管理的文件放入暂存区域(git add)
3. 将暂存区域的文件提交到git仓库(git commit)

### Git文件操作

> 文件的状态

- **Untracked**： 未跟踪，此文件在文件夹中，但是并没有加入到git库，不参与版本控制，通过`git add`状态变为`Staged`。
- **Unmodify**： 文件已经入库，未修改，即版本库中的文件快照内容与文件夹中的完全一致，这种类型的文件有两种去处，如果被修改则变为`Modified`； 如果使用`git rm`移出版本库，则变为`Untracked`文件。
- **Modified**： 文件已经修改，但仅是修改并没有进行其它的操作，该种文件同样有两种去处，通过`git add`可进入`Staged`状态；使用`git checkout`则丢弃修改，返回`Unmodify`状态。
- **Staged**： 暂存状态，执行`git commit`将修改同步到库中，这是库中的文件与本地文件又变为一致，文件为`Unmodify`状态；执行`git reset HEAD filename`则取消暂存，文件状态为`Modified`。

> 查看文件状态

通过`git status`命令查看文件的状态

> 忽略文件

在主目录下建立`.gitignore`文件，其规则如下：
1. 忽略文件中的空行或以(#)开始的行将会被忽略。
2. 可以使用Linux的通配符。
3. 如果名称的最前面有一个(!)，表示例外规则，将不被忽略。
4. 如果名称的最前面是一个(/)，表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5. 如果名称的最后面有一个(/)，则表示要忽略的是该名称下的字目录而非文件（默认文件和目录都忽略）。

```bash
*.txt       #忽略所有.txt结尾的文件
!lib.txt    #但lib.txt除外
/temp       #仅忽略项目根目录下的文件，但不包括其它目录temp
build/      #忽略build/目录下的所有文件
doc/*.txt   #会忽略doc/notes.txt但不包括doc/server/arch.txt
```

### Git分支

> 相关命令

```bash
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但仍然停留在当前分支
git branch [branch name]

# 新建一个分支，并切换到该分支
git checkout -b [branch name]

# 合并指定分支到当前分支
git merge [branch]

# 删除分支
git branch -d [branch name]

# 删除远程分支
git push origin --delete [branch name]
git branch -dr [remote.branch]
```

### Git命令

`git config -l` 查看配置

