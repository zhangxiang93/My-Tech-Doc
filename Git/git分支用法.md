#### 分支的基本用法
1. 如果想保存该分支，并后期方便更新，可以`push`到远程，作为远程分支保存分支代码，执行`git push origin 分支名称
然后`git pull` 会提示`无tracking信息`，此时，执行`git branch --set-upstream-to=origin/分支名称`，即可以执行`git pull`了，当前的代码就是该分支的代码。
或者可以执行`git push origin -u 分支名称`，跟上面的效果一样
2. 如果想删除远程分支执行`git push origin --delete 分支名称`,如果还想删除本地分支的话`git branch -d 分支名称`
3. 如果想查看远程分支，`git branch -a`，如果想查看分支最近的提交信息，`git branch -av`
4. 如果想重命名远程分支，先删除远程分支，再重命名本地分支`git branch -m 原来分支名称  重命名的分支名称`，然后再推送到远程。

#### 创建切换到本地分支
`git checkout testing`

#### 开发完成提交
把开发完的功能代码，提交到暂存区
`git add .`
`git commit -m 'made a change'`

#### 切换回主分支
`git checkout master`
此时相当于位于代码的基础版本，可以继续创建其他分支去同时开发更多的功能

#### 将testing分支合并到主分支
切换到master分支
`git merge testing`
把testing的代码合并到master分支上，然后push到远程主分支

#### 完成
如果需要多个人对分支进行再开发，就需要建立远程仓库的分支testing，然后pull到本地，开发完，再push到远程分支

`注意`: 新建的分支，必须先push到远程分支上，再合并

#### 原理
![如图](http://p8.qhimg.com/t018e4d2ec3cea75033.png)

切换分支就相当于`HEAD`指针指向那个分支
当前分支的改动属于当前版本的一个改动，不影响其他版本 

#### 如何强制合并，冲突太多的情况下
如果分支可以覆盖master来推送
可以
```
git checkout master
git reset  --hard 分支名称
git push origin master --force
```
就可以强制覆盖了