#### 问题
在每次使用`git push`的时候都需要输入用户和密码，是不是觉得很麻烦，为了提高效率
我们可以不需要输入密码就直接提交，我们知道`Github`获取远程库时，有`ssh`方式和`https`方式
![](http://p9.qhimg.com/t0199d7dcb4ca34a89d.png)

#### 原因
两个方式的`url`地址不同，认证方式也不同。使用`ssh`时保存密钥对以后可以不再输入帐号密码，
而`https`却不能。所以如果想要不再输入帐号密码，

#### 解决
一种方式就是在`git clone`的时候使用`ssh`方式
另一种方式就是改变`remote`远程`url`，如下：
```
$ git remote rm origin  
$ git remote add origin git@github.com:yourself.git  
```