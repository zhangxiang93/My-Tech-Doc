#### 介绍
`Yarn` 是 `Facebook`, `Google`, `Exponent` 和 `Tilde` 开发的一款新的 `JavaScript` 包管理工具。就像我们可以从官方文档了解那样，它的目的是解决这些团队使用 `npm` 面临的少数问题，即：

* 安装的时候无法保证速度/一致性
* 安全问题，因为 `npm` 安装时允许运行代码

#### 创建项目
```
yarn init
```

#### 安装依赖包
```
yarn == yarn install
```

#### 其他命令
```
yarn add 包名 [--dev/D]      添加依赖包安装
yarn bin                    显示yarn安装目录
yarn cache  [ls/dir/clean]  显示包缓存（列表/路径/清理）
yarn clean                  清理不需要的依赖文件
yarn remove                 卸载包
yarn upgrade                升级依赖包
```
