##### 简单的办法一
```
以www.xunlei.com为例，得到如下结果：
      [root@UFO bbiinn]# wget -S www.xunlei.com
      --2012-04-27 01:00:48--  http://www.xunlei.com/
     正在解析主机 www.xunlei.com... 119.147.41.83, 121.14.82.140, 121.14.82.141, ...
     Connecting to www.xunlei.com|119.147.41.83|:80... 已连接。
     已发出 HTTP 请求，正在等待回应...
      HTTP/1.1 200 OK
      Server: nginx/1.0.11
      Date: Thu, 26 Apr 2012 09:00:51 GMT
      Content-Type: text/html
      Connection: close
      Vary: Accept-Encoding
      Expires: Thu, 26 Apr 2012 10:00:51 GMT
      Cache-Control: max-age=3600
```

##### 法二：
```
[root@UFO bbiinn]# curl -I www.xunlei.com
      HTTP/1.1 200 OK
      Server: nginx/0.7.69
      Date: Thu, 26 Apr 2012 08:40:05 GMT
      Content-Type: text/html
      Connection: keep-alive
      Vary: Accept-Encoding
      Expires: Thu, 26 Apr 2012 09:40:05 GMT
      Cache-Control: max-age=3600
```
