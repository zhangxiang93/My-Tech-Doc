#### 安装
 `npm install -g dev-ip  --registry=https://registry.npm.taobao.org --verbose `

后面的镜像可加可不加

#### 运行
获取当前真实的ip
```
$dev-ip
['10.18.60.101']
```

#### 工程里的使用
```
var devip = require('dev-ip)
devip() //输出ip值
```