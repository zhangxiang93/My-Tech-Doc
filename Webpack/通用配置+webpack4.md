#### webpack.config.js

版本：
```
"webpack": "^4.16.2",
"webpack-cli": "^3.1.0",
"webpack-dev-server": "^3.1.5"
```
框架：
```
"react": "^16.4.1",
"react-dom": "^16.4.1"
```

#### 通用配置
```
const path = require("path")
const webpack = require("webpack")
const chalk = require("chalk")
const HtmlWebPackPlugin = require("html-webpack-plugin")
const CleanWebpackPlugin = require("clean-webpack-plugin")
const UglifyjsWebpackPlugin = require("uglifyjs-webpack-plugin")
const ExtractTextWebpackPlugin = require("extract-text-webpack-plugin")
const ProgressBarPlugin = require('progress-bar-webpack-plugin')

module.exports = {
    entry: {
        main: "./src/index.js",
        base: "./src/base.js"  //两个entry(都引用了react和react-dom)
    },
    output: {
        filename: "static/js/[name].js",
        path: path.resolve(__dirname, "dist"),
        publicPath: "/"
    },
    module: {
        rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /node_modules/,
                use: {
                    loader: "babel-loader"
                }
            },
            {
                test: /\.html$/,
                use: {
                    loader: "html-loader"
                }
            },
            {
                test: /\.(scss|css)$/,
                use: ExtractTextWebpackPlugin.extract({
                    fallback: 'style-loader',
                    use: ['css-loader', 'postcss-loader', 'sass-loader']
                })
            }
        ]
    },
    plugins: [
        new CleanWebpackPlugin(["dist"]),
        new HtmlWebPackPlugin({
            template: path.resolve(__dirname, "src", "index.html"), //模板
            filename: "index.html",
            chunks: ["index", "common"], //多页面该项用于不同页面注入trunk不同
            //excludeChunks: ["index"], //跟chunks相反，该页面不注入谁
            /**
             *  demo
             *  new HtmlWebpackPlugin({
             *      template: 'src/html/index.html',
             *      excludeChunks: ['list', 'detail']
             *  }),
             *  new HtmlWebpackPlugin({
             *      filename: 'list.html',
             *      template: 'src/html/list.html',
             *      thunks: ['common', 'list']
             *  }), 
             *  new HtmlWebpackPlugin({
             *  filename: 'detail.html',
             *  template: 'src/html/detail.html',
             *  thunks: ['common', 'detail']
             *  })
             *  注：应用中配置了三个入口页面：index.html、list.html、detail.html；并且每个页面注入的thunk不尽相同；类似如果多页面应用，就需要为每个页面配置一个
             */
            hash: true, //防止缓存,静态资源添加hash参数
            minify:{
                removeAttributeQuotes: true //压缩 去掉引号
            }
        }),
        new HtmlWebPackPlugin({
            template: path.resolve(__dirname, "src", "base.html"),
            filename: 'base.html',
            hash: true,
            chunks: ['base', 'common'],
            minify: {
              removeAttributeQuotes: true
            }
        }),
        new ExtractTextWebpackPlugin({
            filename: 'static/css/[name].[hash].css'
        }),
        new webpack.HotModuleReplacementPlugin(),
        new webpack.NamedModulesPlugin(), //用户名替代id
        new UglifyjsWebpackPlugin(), //js压缩
        new ProgressBarPlugin({
            format: '  build [:bar] ' + chalk.green.bold(':percent') + ' (:elapsed seconds)'
        }) //显示打包进度
    ],
    optimization: {
        splitChunks: {
            cacheGroups: {
                commons: {
                    chunks: 'all',
                    minChunks: 2,
                    maxInitialRequests: 5, 
                    minSize: 0,
                    name: 'common'
                }
            }
        }
    }
}
```
这里`extract-text-webpack-plugin`在`webpack4`里已经不支持早期版本了。如果仍然要用，安装的时候可以加上`@next`，如下
```
yarn add extract-text-webpack-plugin@next -D
```
也可以用`mini-css-extract-plugin`，如下
```
yarn add mini-css-extract-plugin -D
```

#### 编译
![图示](../photos/webpack.png)

这里`common.js`就是两个入口文件公共部门，分割成`chunk`，避免重复加载。
