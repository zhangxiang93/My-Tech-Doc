> 首语： 就像在浏览器中使用jquery一样方便。

#### 安装模块cheerio

`npm install cheerio`

可以用淘宝镜像   

`--registry=https://registry.npm.taobao.org --verbose`

#### 抓取导出网页内容代码
```
新建curl.html
代码：
var http = require("http");
 
// Utility function that downloads a URL and invokes
// callback with the data.
function download(url, callback) {
  http.get(url, function(res) {
    var data = "";
    res.on('data', function (chunk) {
      data += chunk;
    });
    res.on("end", function() {
      callback(data);
    });
  }).on("error", function() {
    callback(null);
  });
}
 
exports.download = download;
```

#### 提取自己需要的部分内容代码
```
新建index.js
代码如下：
var cheerio = require("cheerio");
var server = require("./curl");
 
var url = "http://v.163.com/special/opencourse/englishs1.html"
 
server.download(url, function(data) {
  if (data) {
    //console.log(data);
 
    var $ = cheerio.load(data);
    $("a.downbtn").each(function(i, e) {
        console.log($(e).attr("href"));
    });
 
    console.log("done");
  } else {
      console.log("error");
  }
});
```

#### 运行

`node index.js`

#### 结果
