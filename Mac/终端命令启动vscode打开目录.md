#### 设置用户环境变量
`mac linux` 会在用户目录下也就是` ~ `这个目录是用 `./bash_profile` 管理环境变量。
```
vim ~/.bash_profile
vim ~/.zshrc(如果用zsh的话)
#输入以下内容
code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $* ;}
#保存退出
code . #启动vscode，当前目录也被打开了
```
就这么简单