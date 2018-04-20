### node.js环境
[Node.js 官网：https://nodejs.org/en/ ](https://nodejs.org/en/)

下载最新版，这里是`windows64位8.11.1LTS`
然后双击默认安装
打开命令窗口，输入
```
node -v
```
如果显示`node`版本号，那么说明安装成功。

### git环境
[Git 官网：https://git-scm.com/](https://git-scm.com/)

下载安装包，默认安装。

右键打开`Git Bush Here`，输入`git --version`，出现版本号说明`Git`安装成功。

### Github注册和配置
[Github注册：https://github.com/](https://github.com/)

注册成功后，创建一个新的仓库，仓库名为你的用户名`yourname`，例如`zhangxiang93/zhangxiang93.github.io`。
访问 `yourname.github.io`，如果可以正常访问，那么 `Github` 的配置已经结束了。

### HEXO安装配置
`Hexo` 是一个快速、简洁且高效的博客框架，使用 `Markdown`（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

[官方文档:https://hexo.io/zh-cn/](https://hexo.io/zh-cn/)

1. 安装
```
npm install hexo-cli -g
```
查看`hexo`版本号
```
hexo version
```
![](http://p9.qhimg.com/t01beb3bdb5bb149310.png)

安装完成

2. 创建blog文件夹
```
hexo init bxm0927.github.io
cd bxm0927.github.io
npm install
```

完成的文件夹目录如下:
```
.
├── .deploy         #需要部署的文件
├── node_modules    #Hexo插件
├── public          #生成的静态网页文件
├── scaffolds       #模板
├── source          #博客正文和其他源文件，404、favicon、CNAME 都应该放在这里
| ├── _drafts       #草稿
| └── _posts        #文章
├── themes          #主题
├── _config.yml     #全局配置文件
└── package.json    #npm 依赖等
```

3. 运行服务
```
hexo server
```
or
```
hexo s
```
网页地址栏输入`http://localhost:4000`，如果能够正常访问，则说明 `Hexo` 本地博客已经搭建起来了.(只是本地)
如果提示找不到命令，那么需要安装一下`server`
```
sudo npm install hexo-server --save
```

### 关联Hexo与Github
生成与`github`关联的`ssh`密匙，参考我的`git`文章：[生成ssh密匙](https://github.com/zhangxiang93/My-Tech-Doc/blob/master/Git/%E7%94%9F%E6%88%90ssh%E5%AF%86%E5%8C%99.md)

把`ssh-key`添加到`github`，然后输入
```
ssh -T git@github.com
```
反馈
```
The authenticity of host ‘github.com (207.97.227.239)’ can’t be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?
```
输入`yes`
```
Hi aierui! You've successfully authenticated, but GitHub does not provide shell access.
```
说明成功。
而后，`Git `会根据用户的名字和邮箱来记录提交。`GitHub` 也是用这些信息来做权限的处理，输入下面的代码进行个人信息的设置，把名称和邮箱替换成你自己的。
```
git config --global user.name "zhangxiang93"
git config --global user.email "zhangxiang93@163.com"
```
配置`Deloyment`，在`_config.yml`中修改`git`地址
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:zhangxiang93/zhangxiang93.github.io.git
  branch: master
```

本地文件提交到`Github`
```
// 删除旧的 public 文件
hexo clean
// 生成新的 public 文件
hexo g
// 开始部署
hexo d
```

然后，浏览器输入地址`zhangxiang93.github.io`，看到`hexo`引导页，即说明成功关联。

### README.md文件部署
* `Hexo`原理就是`hexo`在执行`hexo generate`时会在本地先把博客生成的一套静态站点放到`public`文件夹中，在执行`hexo deploy`时将其复制到`.deploy`文件夹中。
* `hexo`默认情况下会把所有`md`文件解析成`html`文件，所以即使你在线生成了 `README. md`，它也会在你下一次部署时被`删去`。
* 在执行`hexo deploy`前把在本地写好的`README.md`文件复制到`.deploy`文件夹中，再去执行`hexo deploy`。

### 自定义域名
这里可以看个人意愿，如果不想额外支出，就访问`github`默认地址也可以。
1. 阿里云买个域名，博客地址重定向到该域名（即绑定），我自己的：[zxxiang.top](http://zxxiang.top)
2. 在`Github`根目录下新建一个`CNAME`的文本文件，打开文件，输入
```
zxxiang.top
```
不要加`http://`，`CNAME` 一定是在你 `Github` 项目的 `master` 根目录下
3. 进入阿里云域名解析地址，添加解析：
```
记录类型选择 CNAME
主机记录填 www
解析线路选择默认
记录值填 yourname.github.io
TTL值为 10 分钟
再添加一个解析，记录类型 A
主机记录填 www
解析线路选择默认
记录值填你 GitHub 的 ip 地址（在cmd中ping：ping bxm0927.github.com）
```
4. 保存，等待1分钟，访问自己的域名，ok
5. `CNAME`文件在每次`hexo`部署的时候都会被删除，可以安装插件永久保留
```
$ npm install hexo-generator-cname --save
```
之后在`_config.yml`文件里配置
```
plugins:
- hexo-generator-cname
```
这样之后，每次`deploy`之后`CNAME`都是`yoursite.com`，可以添加配置`_config.yml`
```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://zxxiang.top
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:
```

### 发布文章
至此恭喜你的`blog`已经完成，下面我们来发布一篇自己的第一篇博文。
1. 新建
```
hexo new "文章标题"
```
2. 在`source\_posts`文件夹下找到，刚创建的`markdown`文件
3. 文件编辑完以后，发布
```
hexo clean
hexo g
hexo d
```
4. 文章添加标签`tags`
```
tags: [a, b, c]
或
tags:
  - a
  - b
  - c
```
5. 如果文章列表不想全文显示，可以
```
<!--more-->
后面的文章内容都不会显示在列表
```

### 主题NEXT
到这里就满足了，有点早。
我们应该给我们的`blog`，搭配一套酷炫的主题，才符合你高大帅气有才的身份。
这里我推荐`hexo`的最佳`CP`——`NEXT`主题

安装方法参考官网：[NEXT主题安装](http://theme-next.iissnan.com/getting-started.html)

配置文件如图

![](http://p8.qhimg.com/t01fabe5a259b78b8a1.png)

注意区分跟`HEXO`的配置文件`_config.yml`的位置不同。

主题配置参考：[NEXT主题配置](http://theme-next.iissnan.com/theme-settings.html)

更换主题图标：[NEXT主题图标](https://fontawesome.com/icons?d=listing)

详细优化（包括添加评论，打赏）；[NEXT详细优化](https://zhuanlan.zhihu.com/p/33616481)

### 多客户端管理发布博客
你一定有公司家里两台电脑发布文章的需求。下面介绍下操作
##### 公司电脑
1. 备份博客内容到`github`，在`.gitignore`添加
```
/.deploy_git
/public
```
2. 初始化仓库
```
git init
git remote add origin  //为远程仓库地址
```
3. 同步远程仓库
```
git add . #添加目录下所有文件
git commit -m "更新说明" #提交并添加更新说明
git push -u origin master #推送更新到远程仓库
```
##### 家里电脑
1. 安装好`node`、`git`、`ssh`和`hexo`环境，创建好`hexo`文件夹
2. 从`github`上除了/.deploy_git和/public备份的代码pull到本地（其他先从本地删除），执行
```
git init
git remote add origin <server>
git fetch --all
git reset --hard origin/master
```
3. 发布完博客以后，同步，执行
```
git add .
git commit -m 
git push -u origin master  
```

##### 其他办法
可以把代码备份到`云盘`里，然后在另外的`PC`端去搭建环境，代码覆盖即可。（具体操作省略）