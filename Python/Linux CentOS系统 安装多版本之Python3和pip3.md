### 环境
运行命令：`cat /etc/redhat-release`，查看开发机当前系统版本
系统信息： `CentOS Linux release 7.5.1804 (Core)`
当前最新python：`3.6.5`

### 安装python3
1. 准备
```
$ sudo mkdir /usr/local/python3 # 创建安装目录

# 下载 Python 源文件
$ wget --no-check-certificate https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz
# 注意：wget获取https的时候要加上：--no-check-certificate

$ tar -xzvf Python-3.6.5.tgz # 解压缩包

$ cd Python-3.6.5 # 进入解压目录
```
2. 编译
```
$ sudo ./configure --prefix=/usr/local/python3 # 指定创建的目录

$ sudo make

$ sudo make install
```
3. 配置`python2`和`python3`共存

创建`python3`软链接
```
$ sudo ln -s /usr/local/python3/bin/python3 /usr/bin/python3
```
`python`对应`Python 2`，`python3` 来使用 `Python 3`。

### 安装pip

1. 源码安装
```
# 下载源代码
$ wget --no-check-certificate https://github.com/pypa/pip/archive/9.0.1.tar.gz

$ tar -zvxf 9.0.1.tar.gz    # 解压文件

$ cd pip-9.0.1

# 使用 Python 3 安装
$ python3 setup.py install
```
2. 创建软链
```
$sudo ln -s /usr/local/python3/bin/pip /usr/bin/pip3
```
3. 升级`pip`
```
$ pip3 install --upgrade pip
```

安装完成。

### 验证
输入`pip3 list`和`python3 --version`，查看是否可用