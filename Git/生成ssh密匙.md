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

#### 多个key
指定名称保存
```
ssh-keygen -t rsa -f ~/.ssh/id_rsa.note -C 'email地址'
```
本地就会有两个文件`id_rsa.note`和`id_rsa.note.pub`