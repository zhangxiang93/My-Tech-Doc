#### 基本介绍
`Curl`是`Linux`下一个很强大的`http`命令行工具，其功能十分强大。

#### 实践
1. 显示网页`html`代码
```
$ curl http://www.linuxidc.com

回车之后，www.linuxidc.com 的html就稀里哗啦地显示在屏幕上了 
```

2. 下载网页并保存
```
$ curl http://www.linuxidc.com > page.html
保存。如果想显示保存结果进度条，那么
$ curl -o page.html http://www.linuxidc.com
设置代理服务器
$ curl -x 123.45.67.89:1080 -o page.html http://www.linuxidc.com
保存网页同时，保存cookie信息到指定文件
$ curl -x 123.45.67.89:1080 -o page.html -D cookie0001.txt http://www.linuxidc.com
```

3. 指定你访问的浏览器环境（可以骗过服务器）
```
$ curl -A "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)" -x 123.45.67.89:1080 -o page.html -D cookie0001.txt http://www.linuxidc.com

这样，服务器端接到访问的要求，会认为你是一个运行在Windows 2000上的 IE6.0，嘿嘿嘿，其实也许你用的是苹果机呢！
```

4. 指定referer，骗过服务器
```
$ curl -A "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)" -x 123.45.67.89:1080 -e "mail.linuxidc.com" -o page.html -D cookie0001.txt http://www.linuxidc.com

这样，就可以骗对方的服务器，你是从mail.linuxidc.com点击某个链接过来的了
```

5. 下载文件
```
$ curl -o 1.jpg http://cgi2.tky.3web.ne.jp/~zzh/screen1.JPG
如果用大写-O
$ curl -O http://cgi2.tky.3web.ne.jp/~zzh/screen1.JPG

这样，就可以按照服务器上的文件名，自动存在本地了！
$ curl -O http://cgi2.tky.3web.ne.jp/~zzh/screen[1-10].JPG
这个，更方便，就是自动保存10个文件了。例如screen1.jpg、screen2.jpg
``` 
