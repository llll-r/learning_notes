## Git常用命令

## 1. 创建一个版本库

- `git init` 把这个目录变成Git可以管理的仓库
- `git add readme.txt` 将文件添加到仓库
- ` git commit -m "wrote a readme file"` 告诉git, 把文件提交到仓库。  `-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录

`commit`可以一次提交很多文件，所以可以多次`add`不同的文件

## 2. 时光机

### 版本回退

-  ```git status``` 可以让我们时刻掌握仓库当前的状态。（我们已经成功地添加并提交了一个readme.txt文件，现在我们继续修改readme.txt文件）![QQ截图20200915102913](https://i.loli.net/2020/09/15/ay9eRgHlk6qFsKm.png)

上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。

- ```git diff```  查看difference。上面的虽然Git告诉我们`readme.txt`被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周从国外回来，第一天上班时，已经记不清上次怎么修改的`readme.txt`，所以，需要用`git diff`这个命令看看。

![QQ截图20200915103227](https://i.loli.net/2020/09/15/2ReUTrC7S1cnlQ3.png)

-号代表被修改掉的内容， +代表新增加的内容。 知道修改什么内容后，此时就可以继续进行 ```git add```  和```git commit``` 操作。提交后，再用```git status``` 查看状态，Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。 

- `git log`命令显示从最近到最远的提交日志。![QQ截图20200915110116](https://i.loli.net/2020/09/15/5VeJHYrOoBgDxsk.png)

  Git中，用`HEAD`表示当前版本，也就是最新的提交

- ```git reset --hard 版本号  ```  指定版本号回退 。 版本号没必要写全，前几位就可以了，Git会自动去找。

- `git reflog`用来记录你的每一次命令（查看命令历史）。

  ![QQ截图20200915110946](https://i.loli.net/2020/09/15/CKYIyhcu3nXxfNO.png)

   ##  管理修改

- `git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别

  每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。![QQ截图20200915112702](https://i.loli.net/2020/09/15/hLnxPFSVt1zTRQG.png)

- 场景一：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

- 场景二：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。（用`HEAD`时，表示回到最新的版本）

##  3. 远程仓库

- `git remote add origin 仓库地址(ssh)`  把本地仓库的内容推送到远程仓库。程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的。（使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。）

- `git push -u origin master`  第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

- 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改。

- `git checkout -b dev` 创建dev分支。加上`-b`参数表示创建并切换，相当于以下两条命令：

  1. `git branch dev`

     2 .`git checkout dev`

- `git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

- `git checkout master` 切换到master分支

- `git merge dev` 把dev的工作成果合并到master分支上。

- `git branch -d dev` 删除dev分支。



