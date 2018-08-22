### 本地

`$ ssh-keygen`
`打开/.ssh/id_rsa.pub`

### 开发机

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
测试执行下面命令
```
$ ssh -T git@github.com  
```
提示成功，`ok`。首次会自动写入`known_hosts`文件。

### 多个git仓库key
指定名称保存
```
ssh-keygen -t rsa -C 'Your Email Address' -f ~/.ssh/docSSH  // -C 'Your Email Address'也可以不设置
```
本地就会多两个文件，注意`name`就是你要保存文件的名称，如果不设置的话，默认都是一样的名字，会覆盖
#### 把私钥添加到git
```
ssh-add -l  //检查你之前是否创建代理
```
以上命令若输出 `"Could not open a connection to your authentication agent" `则还没有创建代理。可以先执行以下命令创建代理
```
eval `ssh-agent -s`
```
如输出 `"The agent has no identities"` 则表示没有代理。如果系统有代理，可以执行下面的命令清除代理:
```
ssh-add -D  //清理之前缓存的key
```
然后依次将不同的`ssh`添加代理，执行命令如下：
```
ssh-add ~/.ssh/docSSH
ssh-add ~/.ssh/otherSSH
```
#### 配置config
然后，在`~/.ssh/`下新建`config`文件
```
touch config
subl -a config
```
添加以下内容
```
 # document
 Host docSSH.github.com
 HostName github.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/docSSH

# project
 Host github.com
 HostName github.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa

```

#### 修改远程仓库地址
配置完成后，在连接`github`仓库时，远程库的地址要对应地做一些修改，比如现在添加帐号下的`doc`仓库，则需要这样添加：
```
git remote add origin git@docSSH.github.com:username/doc.git
```

#### 测试ssh
```
ssh -T git@github.com
```
输出`Hi username/doc! You've successfully authenticated, but GitHub does not provide shell access.`，注意这里的`username/doc`必须是当前项目才可以

#### 成功添加
如果添加多个账号，按照同理添加即可