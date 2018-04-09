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
