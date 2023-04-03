# GIT指令

## DEPTH

git的depth是指在克隆一个仓库时，限制历史记录的深度，也就是获取的提交数。使用–depth参数可以减少克隆的仓库大小，加快克隆的速度。但是，如果仓库中有合并提交，那么实际获取的提交数可能会多于指定的深度。

## RECURSIVE

git Recursive是指在使用git命令时，对子模块或者子目录进行递归操作的选项。

例如，使用git fetch --recurse-submodules来获取主项目和所有子模块的更新，或者使用git add -A或者git add --all来将主项目和所有子目录中的文件添加到暂存区。

这样可以方便地管理多个相关的项目或者库。

## CLONE INTO BARE REPO

git clone into bare repo是指使用git clone命令时，加上–bare选项，来创建一个没有工作区和索引的仓库。

这样的仓库只包含.git目录中的数据，通常用于作为远程仓库或者备份。

克隆一个普通的仓库为一个裸仓库的命令是：

​	`git clone --bare /path/to/repo`

这个命令会在当前目录下创建一个以.git为后缀的目录，存放裸仓库的数据。