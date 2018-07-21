#### yarn.lock 文件
用于每次把包的固定版本锁住，便于以后不同机器能保持包的版本一致性
`yarn`的会自动更新，`npm`要重新创建

#### 并行安装
`npm`安装包的时候，会按包的任务顺序一个一个安装
`yarn`会并行安装，提高了性能，速度快了不少

#### 清晰的输出
`yarn`安装任务的时候，输出信息一点不冗余，而且很清晰

![](http://p0.qhimg.com/t01af765b75ea3b010d.png)

#### yarn global
不像 `npm` 添加 `-g` 或 `--global` 可以进行全局安装，`Yarn` 使用的是 `global `前缀。不过与 `npm` 类似，项目依赖`不推荐全局安装`。

`global` 前缀只能用于 `yarn add`, `yarn bin`, `yarn ls` 和 `yarn remove`，除 `yarn add` 外，这些命令都和 `npm `等效。

#### yarn upgrade
会根据`package.json`里的设定更新到最新版本。
`npm`必须要删除`node_moudles`，然后执行`npm install`才可以，比较麻烦