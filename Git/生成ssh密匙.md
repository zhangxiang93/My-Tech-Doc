#### 本地

`$ ssh-keygen`
`打开/.ssh/id_rsa.pub`

#### 开发机

```
$ cd ~
$ ssh-keygen -t rsa -C "youremail@domain.com"
```

然后
```
$ cd ~/.ssh
~/.ssh $ ls
id_rsa      id_rsa.pub
```
测试
```
$ ssh -T git@github.com
```
提示成功，`ok`

#### 多个git帐号key
指定名称保存
```
ssh-keygen -t rsa -C 'Your Email Address' -f ~/.ssh/own_rsa  // -C 'Your Email Address'也可以不设置
```
本地就会多两个文件，注意`name`j就是你要保存文件的名称，如果不设置的话，默认都是一样的名字，容易覆盖

然后，在`~/.ssh/`下新建`config`文件
```
touch config
```
添加以下内容
```
 # document
 Host github.com
 HostName github.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/own_rsa
 # gitlib
 Host gitlib.com
 HostName gitlib.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa
```
这里的`own_rsa`，就是你自己`git`用的，另外一个就是公司用的