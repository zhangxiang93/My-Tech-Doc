#### 引用
```
var url = require("url");
var queryString  = require("querystring");
```
`URL`模块
该模块比较简单，方法也只有三个

#### URL各部分说明
对于一个 `URL` 字符串，其组成部分会有所有不同，其中有些部分只有在`URL`字符串中存在时，对应字段才会出现在解析后对象中。以下是一个 `URL `例子：

`http://user:pass@host.com:8080/p/a/t/h?query=string#hash`

解析后对象字段如下：
```
href: 解析前的完整原始 URL，协议名和主机名已转为小写
例如: 'http://user:pass@host.com:8080/p/a/t/h?query=string#hash'

protocol: 请求协议，小写
例如: 'http:'

slashes: 协议的“：”号后是否有“/”
例如: true or false

host: URL主机名，包括端口信息，小写
例如: 'host.com:8080'

auth: URL中的认证信息
例如: 'user:pass'

hostname: 主机名，小写
例如: 'host.com'

port: 主机的端口号
例如: '8080'

pathname: URL中路径
例如: '/p/a/t/h'

search: 查询对象，即：queryString，包括之前的问号“?”
例如: '?query=string'

path: pathname 和 search的合集
例如: '/p/a/t/h?query=string'

query: 查询字符串中的参数部分（问号后面部分字符串），或者使用 querystring.parse() 解析后返回的对象
例如: 'query=string' or {'query':'string'}

hash: 锚点部分（即：“#”及其后的部分）
例如: '#hash'
```
#### 将`URL`字符串转换为对象：`url.parse(urlStr[, parseQueryString][, slashesDenoteHost])`
`url.parse()`方法用于解析`URL`对象，解析后返回一个`JSON`对象。示例如下：
```
var url = require('url');

var urlString = 'http://user:pass@host.com:8080/p/a/t/h?query=string#hash';
var result = url.parse(urlString);
console.log(result);

//输出结果如下
{ protocol: 'http:',
  slashes: true,
  auth: 'user:pass',
  host: 'host.com:8080',
  port: '8080',
  hostname: 'host.com',
  hash: '#hash',
  search: '?query=string',
  query: 'query=string',
  pathname: '/p/a/t/h',
  path: '/p/a/t/h?query=string',
  href: 'http://user:pass@host.com:8080/p/a/t/h?query=string#hash' 
}
```
//第二个可选参数设置为true时，会使用querystring模块来解析URL中德查询字符串部分，默认为 false。

//输出结果如下
```
{ protocol: 'http:',
  slashes: true,
  auth: 'user:pass',
  host: 'host.com:8080',
  port: '8080',
  hostname: 'host.com',
  hash: '#hash',
  search: '?query=string',
  query: {query:"string"},
  pathname: '/p/a/t/h',
  path: '/p/a/t/h?query=string',
  href: 'http://user:pass@host.com:8080/p/a/t/h?query=string#hash' 
}
```
//第三个可参数设置为 `true`时，会把诸如 `//foo/bar` 这样的`URL`解析为 `{ host: 'foo', pathname: '/bar' }` 而不是 `{ pathname: '//foo/bar' }`。 默认为 `false`。

#### 将对象格式化为URL字符串：`url.format(urlObj)`

`url.resolve()`用于格式化`URL`对象。输入一个 `URL `对象，返回格式化后的 `URL` 字符串。
示例如下：
```
var url = require('url');

var urlObj = { 
  protocol: 'http:',
    slashes: true,
    hostname: 'itbilu.com',
    port: 80,
    hash: '#hash',
    search: '?query=string',
    path: '/nodejs?query=string'
}
var result = url.format(urlObj);
console.log(result);

//输出结果如下
http://itbilu.com:80?query=string#hash

/*
*传入的URL对象会做以下处理：
*
*href 属性会被忽略
*protocol无论是否有末尾的 : (冒号)，会同样的处理
*这些协议包括 http, https, ftp, gopher, file 后缀是 :// (冒号-斜杠-斜杠).
*所有其他的协议如 mailto, xmpp, aim, sftp, foo, 等 会加上后缀 : (冒号)
*auth 如果有将会出现.
*hostname 如果 host 属性没被定义，则会使用此属性.
*port 如果 host 属性没被定义，则会使用此属性.
*host 优先使用，将会替代 hostname 和port
*pathname 将会同样处理无论结尾是否有/ (斜杠)
*search 将会替代 query属性
*query (object类型; 详细请看 querystring) 如果没有 search,将会使用此属性.
*search 无论前面是否有 ? (问号)，都会同样的处理
*hash无论前面是否有# (井号, 锚点)，都会同样处理
*/
```

#### URL路径处理：`url.resolve(from, to)`
`url.resolve()`方法用于处理URL路径，也可以用于处理锚点。示例如下：
```
url.resolve('/one/two/three', 'four')         // '/one/two/four'
url.resolve('http://example.com/', '/one')    // 'http://example.com/one'
url.resolve('http://example.com/one', '/two') // 'http://example.com/two'
```
#### queryString 模块
查询字符串主要由两个方法和内置格式化方法组成，一个是将对象转换为字符串，一个则是相反，将字符串转换为对象：

1. querystring.stringify(obj, [sep], [eq])：
将`JSON`对象格式化为查询字符串格式的字符串，默认的分隔符为：`“&”和“=”`，具体可以看一下以下代码：
```
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' })

// returns
'foo=bar&baz=qux&baz=quux&corge='
querystring.stringify({foo: 'bar', baz: 'qux'}, ';', ':')
// returns
'foo:bar;baz:qux'
```
2. querystring.parse(str, [sep], [eq], [options])：
根据`“&”`和`“=”`将字符串进行分割，反序列化为`JSON`对象，而`options`包含的`maxKeys`默认设置为`1000`，如果将其设置为`0`则表示没这个限制。
```
querystring.parse('foo=bar&baz=qux&baz=quux&corge')

// returns
{ foo: 'bar', baz: ['qux', 'quux'], corge: '' }
```
3. querystring.escape，querystring.unescape：
这两个内置方法，分别在上述两个方法的内置使用，如果有需要分别格式化和解码`URL`字符串。
```
QueryString模块和Url模块之间的关系
                        url.parse(string).query
                                           |
           url.parse(string).pathname      |
                       |                   |
                       |                   |
                     ------ -------------------
http://localhost:8888/start?foo=bar&hello=world
                                ---       -----
                                 |          |
                                 |          |
              querystring(string)["foo"]    |
                                            |
                         querystring(string)["hello"]
```
