### 介绍
此命令集合版本为 `1.11.1` 及以上

### 基础类
#### 查看docker信息
```
# 查看docker版本
docker version

# 显示docker系统的信息
docker info

# 日志信息
docker logs

# 启动关闭docker
sudo service docker start|stop
```
---
### 日志类
#### 查看容器日志
```
docker logs -f <容器名orID>
```
#### `docker daemon` 日志位置
```
根据系统不同各不相同

* Ubuntu - /var/log/upstart/docker.log
* Boot2Docker - /var/log/docker.log
* Debian GNU/Linux - /var/log/daemon.log
* CentOS - /var/log/daemon.log | grep docker
* Fedora - journalctl -u docker.service
* Red Hat Enterprise Linux Server - /var/log/messages | grep docker
```
#### docker ps没有响应 日志查询
```
# grep 所有容器的config.json
docker logs [conID]

# 确认问题后
# 该config.json 中有该容器1号进程的pid
kill -9 pid
```
---
### 容器类
`docker`容器可以理解为在沙盒中运行的进程。

> 这个沙盒包含了该进程运行所必须的资源，包括文件系统、系统类库、`shell` 环境等等。但这个沙盒默认是不会运行任何程序的。你需要在沙盒中运行一个进程来启动某一个容器。这个进程是该容器的唯一进程，所以当该进程结束的时候，容器也会完全的停止。


#### 查看容器信息
```
# 查看当前运行的容器
docker ps

# 查看全部容器
docker ps -a

# 查看全部容器的id和信息
docker ps -a -q

# 查看一个正在运行容器进程，支持 ps 命令参数
docker top

# 查看容器的示例id
sudo docker inspect -f  '{{.Id}}' [id]

# 检查镜像或者容器的参数，默认返回 JSON 格式
docker inspect

# 返回 ubuntu:14.04  镜像的 docker 版本
docker inspect --format '{{.DockerVersion}}' ubuntu:14.04
```
#### 容器同步命令
```
# 保存对容器的修改
docker commit

# 对比容器的改动
docker diff

# 附加到一个运行的容器上
docker attach
```
#### 容器操作命令
##### 创建删除容器
```
# 创建一个容器命名为 test 使用镜像daocloud.io/library/ubuntu
docker create -it --name test daocloud.io/library/ubuntu

# 创建并启动一个容器 名为 test 使用镜像daocloud.io/library/ubuntu
docker run --name test daocloud.io/library/ubuntu

# 删除一个容器
docker rm [容器id]

# 删除所有容器
docker rm `docker ps -a -q`

# 根据Dockerfile 构建
docker build -t [image_name] [Dockerfile_path]
```
##### docker容器随系统自启
```
docker run --restart=always
```
* no – 默认值，如果容器挂掉不自动重启
* on-failure – 当容器以非 0 码退出时重启容器,同时可接受一个可选的最大重启次数参数 (e.g. on-failure:10).
* always – 不管退出码是多少都要重启
##### 容器资源限制参数
```
# 限制内存最大使用
-m 1024m --memory-swap=1024m

# 限制容器使用CPU
--cpuset-cpus="0,1"
```
#### 把一个正在运行的容器保存为镜像
```
docker commit <CONTAIN-ID> <IMAGE-NAME>
```
#### 启动停止容器等操作
```
# 启动|停止|重启 某一容器的所有进程
docker start|stop|restart [id]

# 暂停|恢复 某一容器的所有进程
docker pause|unpause [id]

# 杀死一个或多个指定容器进程
docker kill -s KILL [id]

# 停止全部运行的容器
docker stop `docker ps -q`

# 杀掉全部运行的容器
docker kill -s KILL `docker ps -q`
```
#### 交互式进入容器
```
sudo docker exec -it {{containerName or containerID}} bash
```
#### 查看容器的root用户密码
```
docker logs <容器名orID> 2>&1 | grep '^User: ' | tail -n1
```
因为Docker容器启动时的root用户的密码是随机分配的。所以，通过这种方式就可以得到容器的root用户的密码了

#### 容器于宿主拷贝文件
```
#本地上传
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH

# 本地文件上传到对应容器的目录
docker cp local.sh [CONTAINERid]:[TagPath]
```
> 此命令为高版本docker才有，当然1.11+肯定包含


#### 运行一个新容器，同时为它命名、端口映射、文件夹映射
以`redmine`镜像为例
```
docker run --name redmine -p 9003:80 -p 9023:22 -d -v /var/redmine/files:/redmine/files -v /var/redmine/mysql:/var/lib/mysql sameersbn/redmine
```
#### 一个容器连接到另一个容器
```
docker run -i -t --name sonar -d -link mmysql:db  tpires/sonar-server sonar
```
#### 导入导出容器
```
# 导入，支持远程文件 .tar, .tar.gz, .tgz, .bzip, .tar.xz, .txz
docker import

# 导出
docker export [id] >~/Downloads/ubuntu_nexus.tar
```
> 导出后导入（exported-imported)）的容器会丢失所有的提交历史，无法回滚。

---
### 镜像操作
#### 远程镜像
```
docker login
```
```
docker search
# 搜索处收藏数不小于 3 ，并且能够自动化构建的  django 镜像，并且完整显示镜像描述
docker search -s 3 --automated --no-trunc django

docker pull
# 拉取ubuntu最新的镜像
docker pull ubuntu:latest

# 服务器拉取个人动态，可选择时间区间
docker events
# 拉取个人从 2015/07/20 到 2015/08/08 的个人动态
docker events --since="20150720" --until="20150808"
```
#### 镜像同步操作
```
# 标记本地镜像，将其归入某一仓库
docker tag

# 将 ID 为 5db5f84x1261 的容器标记为 mine/lnmp:0.2 镜像
docker tag 5db5f84x1261 mine/lnmp:0.2

# 将镜像推送至远程仓库，默认为 Docker Hub
docker push
```
#### 本地镜像
```
# 列出本地所有镜像
docker images

# 本地镜像名为 ubuntu 的所有镜像
docker images ubuntu

# 查看指定镜像的创建历史
docker history [id]

# 本地移除一个或多个指定的镜像
docker rmi

# 移除本地全部镜像
docker rmi `docker images -a -q`

# 指定镜像保存成 tar 归档文件， docker load 的逆操作
docker save

# 将镜像 ubuntu:14.04 保存为 ubuntu14.04.tar 文件
docker save -o ubuntu14.04.tar ubuntu:14.04

# 从 tar 镜像归档中载入镜像， docker save 的逆操作
docker load

# 上面命令的意思是将 ubuntu14.04.tar 文件载入镜像中
docker load -i ubuntu14.04.tar
docker load < /home/save.tar

# 构建自己的镜像
docker build -t <镜像名> <Dockerfile路径>
docker build -t xx/gitlab .
```
> 保存后再加载（saved-loaded）的镜像不会丢失提交历史和层，可以回滚


#### 重新查看container的stdout
```
# 启动top命令，后台运行
$ ID=$(sudo docker run -d ubuntu /usr/bin/top -b)

# 获取正在running的container的输出
$ sudo docker attach $ID
top - 02:05:52 up  3:05,  0 users,  load average: 0.01, 0.02, 0.05
Tasks:  1 total,  1 running,  0 sleeping,  0 stopped,  0 zombie
Cpu(s):  0.1%us,  0.2%sy,  0.0%ni, 99.7%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:    373572k total,  355560k used,    18012k free,    27872k buffers
Swap:  786428k total,        0k used,  786428k free,  221740k cached
^C$

$ sudo docker stop $ID
```
#### docker run
#### 后台运行(-d)、并暴露端口
```
docker run -d -p 127.0.0.1:33301:22 centos6-ssh
```
#### `run` 命令详解
```  
03.  -d, --detach=false         指定容器运行于前台还是后台，默认为false     
04.  -i, --interactive=false   打开STDIN，用于控制台交互    
05.  -t, --tty=false            分配tty设备，该可以支持终端登录，默认为false    
06.  -u, --user=""              指定容器的用户    
07.  -a, --attach=[]            登录容器（必须是以docker run -d启动的容器）  
08.  -w, --workdir=""           指定容器的工作目录   
09.  -c, --cpu-shares=0        设置容器CPU权重，在CPU共享场景使用    
10.  -e, --env=[]               指定环境变量，容器中可以使用该环境变量    
11.  -m, --memory=""            指定容器的内存上限    
12.  -P, --publish-all=false    指定容器暴露的端口    
13.  -p, --publish=[]           指定容器暴露的端口   
14.  -h, --hostname=""          指定容器的主机名    
15.  -v, --volume=[]            给容器挂载存储卷，挂载到容器的某个目录    
16.  --volumes-from=[]          给容器挂载其他容器上的卷，挂载到容器的某个目录  
17.  --cap-add=[]               添加权限，权限清单详见：http://linux.die.net/man/7/capabilities    
18.  --cap-drop=[]              删除权限，权限清单详见：http://linux.die.net/man/7/capabilities    
19.  --cidfile=""               运行容器后，在指定文件中写入容器PID值，一种典型的监控系统用法    
20.  --cpuset=""                设置容器可以使用哪些CPU，此参数可以用来容器独占CPU    
21.  --device=[]                添加主机设备给容器，相当于设备直通    
22.  --dns=[]                   指定容器的dns服务器    
23.  --dns-search=[]            指定容器的dns搜索域名，写入到容器的/etc/resolv.conf文件    
24.  --entrypoint=""            覆盖image的入口点    
25.  --env-file=[]              指定环境变量文件，文件格式为每行一个环境变量    
26.  --expose=[]                指定容器暴露的端口，即修改镜像的暴露端口    
27.  --link=[]                  指定容器间的关联，使用其他容器的IP、env等信息    
28.  --lxc-conf=[]              指定容器的配置文件，只有在指定--exec-driver=lxc时使用    
29.  --name=""                  指定容器名字，后续可以通过名字进行容器管理，links特性需要使用名字    
30.  --net="bridge"             容器网络设置:  
31.                                bridge 使用docker daemon指定的网桥       
32.                                host    //容器使用主机的网络    
33.                                container:NAME_or_ID  >//使用其他容器的网路，共享IP和PORT等网络资源    
34.                                none 容器使用自己的网络（类似--net=bridge），但是不进行配置   
35.  --privileged=false         指定容器是否为特权容器，特权容器拥有所有的capabilities    
36.  --restart="no"             指定容器停止后的重启策略:  
37.                                no：容器退出时不重启    
38.                                on-failure：容器故障退出（返回值非零）时重启   
39.                                always：容器退出时总是重启    
40.  --rm=false                 指定容器停止后自动删除容器(不支持以docker run -d启动的容器)    
41.  --sig-proxy=true           设置由代理接受并处理信号，但是SIGCHLD、SIGSTOP和SIGKILL不能被代理
```

---
### 实例
##### 使用`docker`镜像`nginx:latest`以后台模式启动一个容器,并将容器命名为`mynginx`
```
docker run --name mynginx -d nginx:latest
```

##### 使用镜像`nginx:latest`以后台模式启动一个容器,并将容器的`80`端口映射到主机随机端口
```
docker run -P -d nginx:latest  
```

##### 使用镜像`nginx:latest`以后台模式启动一个容器,将容器的`80`端口映射到主机的`80`端口,主机的目录`/data`映射到容器的`/data`
```
docker run -p 80:80 -v /data:/data -d nginx:latest  
```

##### 使用镜像`nginx:latest`以交互模式启动一个容器,在容器内执行`/bin/bash`命令
```
runoob@runoob:~$ docker run -it nginx:latest /bin/bash  
root@b8573233d675:/# 
```