GitHub的常用指令：

git的工作原理：

![1-git工作原理](D:\LJ\git\git_project\Study_Notes\img\1-git工作原理.png)

1、克隆代码：  http地址：git clone http地址；git地址：git  clone  git@

2、git init：初始化版本库，在工作区生成一个.get的隐藏文件夹

​      git  config -l：查看当前get的配置信息

​      在配置信息中新增用户信息：

​              git config  user.name  '用户名'

​              git config user.email  '邮箱'

3、get status：查看工作区的状态，若在工作区新建了一个文件夹，未提交（未从工作区提交到版本库的暂缓区），则会显示红色，

git add 文件名.拓展名即可完成工作区文件提交暂缓区

git add .    :所有文件都添加到暂缓区

git commit -m   "注释：初始化项目，添加document.txt",将暂缓区的文件提交到header指针指向的分支中，默认分支master,

<span style="color:#F00;">清空git终端指令：clear +回车</font></span>

使用 git  diff  文件名：可查看文件修改的最近内容

git log 文件名：查看文件的修改记录

git log ：查看所有文件的详细修改记录

git reflog：查看所有文件的大致修改记录

git reset --hard     HEAD^:退回上一个版本

git reset --hard   指定版本号（前几个序号）：回到指定版本的修改



touch .gitignore: 设置忽略文件

 多人开发：
       将代码提交到远程的服务器 ：git push，其它的开发人员只需要通过 git pull 就可以拿到更新的代码了

多人开发使用Git注意点:
    1.不能将不能运行的代码提交到本地和远程服务器
    2.如果服务器上有其它开发人员的更新内容, 那么我们不能直接通过push将我们的代码提交到服务器（先pull）
      如果服务器上有其它开发人员更新的内容, 我们必须先将其它开发人员更新的内容更新到本地之后才能通过push提交我们的内容
    3.如何我们更新的内容和其它同事更新的内容有冲突(修改了同一个文件的同一行代码), 这个时候需要我们自己手动修改冲突, 修改完冲突之后才能将代码提交到远程服务器。

<span style="color:#F00;">分支的创建</span>

一、如何查看有多少个分支?
    1.通过git branch指令就可以查看当前版本库中有多少个分支
    注意点:
    1.如果当前的版本库是空的, 那么无法查看
    2.如果通过git branch指令查看当前版本库中有多少个分支, 输出的内容中哪一个分支前面有*号
    就代表当前的HEADER指针指向哪一个分支, 我们提交的代码就会提交到指向的分支中

二、如何创建一个分支
    1.通过git branch 分支名称 来创建一个新的分支
    注意点:
    在哪个分支中创建了新的分支, 那么创建出来的新的分支就会继承当前分支的所有状态
    例如:
    在master分支中做了两个操作, 然后在master分支中创建了Dev分支
    那么创建出来的Dev分支就会继承master分支中的这两个操作
    注意点:
    一旦分支被创建出来之后, 分支就是独立的, 分支之间不会相互影响

三、如何切换分支?
    1.通过git switch 分支名称 来修改HEADER指针的指向
    注意点: 只要HEADER指针的指向发生了改变, 那么commit的代码就会发生改变
    HEADER指针指向谁commit提交的代码就提交到谁里面

四、如何将分支提交到远程服务器
    1.通过git branch -r 来查看远程服务器上有多少个分支
    2.首先需要在本地切换到新建的分支中, 然后通过git push指令提交新建的分支到远程的服务器
    git push --set-upstream origin Dev

五、如何合并分支
    可以通过 git merge 分支名称 来合并分支
    例如:
    在master分支中执行  git merge Dev 就代表需要将Dev分支中的代码都合并到master分支中
    例如:
    在Dev分支中执行 git merge master 就代表需要将master分支中的代码都合并到Dev分支中

六、如何删除分支
    1.可以通过git branch -d 分支名称 来删除本地的分支
    2.可以通过git push origin --delete 分支名称 来删除远程服务器的分支

