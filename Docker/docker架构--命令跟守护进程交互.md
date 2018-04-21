### `Docker`架构图

![](http://p7.qhimg.com/t0142a00545c52bb314.jpg)

解释一下上图中的元素:
* `Docker守护进程(docker daemon)`是运行在你的操作系统上的一个服务。目前，它只能运行在`Linux`上，因为它依赖于一些`Linux`内核特性(比如`Cgroup`与`Namespace`)。 但是，也有一些特殊的办法让`Docker`运行在`MacOS`与`Windows`上(运行在`Linux`虚拟机中)。
* `Docker`守护进程提供了`REST API`。许多工具(`Docker`命令行，`Docker Compose`等)都可以通过`REST API`与`Docker守护进程`进行交互，例如创建容器，构建镜像等。
* `Docker命令行(docker CLI)`是与`Docker`守护进程进行交互的主要工具。

### `Docker`是`C/S`架构
`Docker`是`Client/Serve`r架构。其中`Docker`守护进程是服务端，`Docker`命令行是众多客户端之一。事实上，还有很多第三方的`Docker`客户端。

### Docker命令行与守护进程如何交互

![](http://p6.qhimg.com/t010d6cd0b5ded8f8b9.jpg)

从左至右理解上图:
* 最左侧是`Docker客户端`，即`Docker命令行`。我们可以运行各种`Docker`命令，比如构建镜像(`docker build`)，下载镜像(`docker pull`)，运行容器(`docker run`)。`Docker`命令行可以安装在各种操作系统上，例如`Windows`，`MacOS`或者`Linux`服务器。
* 中间是`Docker`主机，`Docker守护进程`运行在上面。`Docker`命令行可以轻松地连接远程的`Docker`主机(给定`IP`和端口即可)。而在`MacOS`与`Windows`上”运行”`Docker`时，`Docker`守护进程事实上运行在`Linux`虚拟机中。这里关键点在于，`Docker`守护进程和命令行可以运行在不同的主机上。
* 最右侧是`Docker`仓库，它也是`Docker`生态系统中的一份子。它是我们下载、上传、存储以及分享`Docker`镜像的地方。`Docker`仓库的细节与本文无关，因此不再赘述。
