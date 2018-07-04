### 阿里云专属
打开
```
https://cr.console.aliyun.com/#/accelerator
```
用账号：`毛毛是条狗93`登录
打开左侧镜像加速，获得自己的专属阿里云镜像加速器专属地址

```
https://4z0uc9bt.mirror.aliyuncs.com
```

### 在mac系统下配置
* 打开`Docker->Preferences...`
* `Insecure registries`配置:`registry.mirrors.aliyuncs.com`
* `Registry mirrors`配置刚刚专属地址那里自己的镜像加速器地址即可.
* 重启`docker`生效

![](http://p2.qhimg.com/t01482c3c2ff373bded.png)

### 验证是否生效
输入
```
$docker info
```
如果看到
```
Registry Mirrors:
https://registry.docker-cn.com/
```
说明配置成功