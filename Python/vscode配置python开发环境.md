#### vscode配置python开发环境
---
打开终端

安装python
```
vscode选择Python插件（找下载最多的）
```
安装最新的pip
```
python -m pip install -U pip
```
然后有了`pip`，就可以安装`python`代码错误提示模块(需要管理员权限)
```
pip install flake8 //检查规则灵活，支持集成额外插件，扩展性强
or
pip install pylint  //不推荐，过于变态，规则定的太死，一般把该项错误提示关掉即可
```
安装完成后
```
文件-》首选项-》设置
"python.linting.flake8Enabled": true
修改这一项即可
如果想关掉pylint错误提示，那就
"python.linting.pylintEnabled": false
```

#### 运行
---

默认按两次`F5`即可在`vscode`里看到运行结果
如果想按一次`F5`就运行，可以在launch.json文件里改配置
```
"stopOnEntry": true,改为 "stopOnEntry": false
```


#### Mac系统上
在`mac`上安装`flake8`要注意，先要安装好`pip`模块
```
sudo easy_install pip
```
然后
```
sudo pip install flake8
```
即可。
`mac`上自带`python`程序。可以输入`python`看一下当前系统里的版本，目前是`2.7`
如果你需要`Mac`配置`python3`，请参考我的另一篇文章：[《mac下多版本python管理》](https://github.com/zhangxiang93/My-Tech-Doc/blob/master/Python/mac%E4%B8%8B%E5%A4%9A%E7%89%88%E6%9C%ACpython%E7%AE%A1%E7%90%86.md)