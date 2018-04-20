#### 注意
千万不要删除`mac`自带的`python`版本，会影响系统部分功能正常运行


#### 版本管理工具pyenv

[文章一：http://zhangzhk.com/2017/10/19/build-python-development-environment-in-mac/](http://zhangzhk.com/2017/10/19/build-python-development-environment-in-mac/)


[文章二：https://github.com/eteplus/blog/issues/4](https://github.com/eteplus/blog/issues/4)



关掉命令窗口，重新打开，即可实现切换

#### 命令
##### 切换版本
```
# 对所有的Shell全局有效，会把版本号写入到~/.pyenv/version文件中
pyenv global 3.6.3

# 只对当前目录有效，会在当前目录创建.python-version文件
pyenv local 3.6.3

# 只在当前会话有效
pyenv shell 3.6.3

# 可通过配置PYENV_VERSION环境变量或编辑~/.python-version文件设置会话默认使用的python版本
echo "3.6.3" > ~/.python-version
# or
echo 'export PYENV_VERSION="3.6.3"' >> ~/.zshrc && source ~/.zshrc

```

##### 重置
```
pyenv shell --unset
pyenv local --unset
```

##### 卸载
```
pyenv uninstall 3.6.3
```

#### 版本切换失效解决
安装了zsh主题以后，用`pyenv`切换`python`版本失效了
解决办法:
打开`~/.zshrc`文件，加入
```
export PYENV_ROOT=~/.pyenv
export PATH=$PYENV_ROOT/shims:$PATH
```
重启下终端即可