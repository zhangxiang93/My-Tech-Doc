##### 文件夹递归查找
`$ grep -r "192.168.1.5" /etc/`   或   `$ grep -R "192.168.1.5" /etc/`

输出：
![](http://p6.qhimg.com/t01d022a1352fbd1f9b.png)

可以禁止文件路径输出：
`$ grep -hR "192.168.1.5" /etc/`
![](http://p9.qhimg.com/t0120b09e2f75fe1794.png)


##### 文本内容查找
`$ grep "boo" file`  file文件中所有包含boo的全部输出。这里还可以加-i，忽略大小写查找
`$ grep -w "boo" file`  强制file文件中是boo的单词输出所在行
`$ egrep -w 'word1|word2' /path/to/file`  file文件中具有两个关键词搜索出所在的行
`$ grep -c 'word' /path/to/file`  只显示匹配到的次数
`$ grep -n 'root' /etc/passwd`  显示匹配的行及行号
`$ grep -v 'bar' /path/to/file`  输出不包含文本的行
`$ grep -l  'main'  *.c`  包含该文本的后缀是.c的文件名输出
`$ grep -l  'main'  *`  包含该文本的当前目录下所有文件的文件名输出
`$ grep --color  'vivek'  /etc/passwd`  包含该文本的该目录下文件的文件名，以及该文本彩色输出

![](http://p9.qhimg.com/t0120b09e2f75fe1794.png)

` *搜索的文本可以加引号也可以不加`

##### 文件位置查找

```
find / -name httpd.conf　　#在根目录下查找文件httpd.conf，表示在整个硬盘查找
find /etc -name '*srm*'　　#使用通配符*(0或者任意多个)。表示在/etc目录下查找文件名中含有字符串‘srm’的文件
find . -name 'srm*' 　　#表示当前目录下查找文件名开头是字符串‘srm’的文件
find / -empty 　　# 查找在系统中为空的文件或者文件夹
find / -amin -10 　　# 查找在系统中最后10分钟访问的文件(access time)
find / -mmin -5 　　# 查找在系统中最后5分钟里修改过的文件(modify time)
find / -mtime -1 　　#查找在系统中最后24小时里修改过的文件
find / -user fred 　　#查找在系统中属于fred这个用户的文件
find / -size +10000c　　#查找出大于10000000字节的文件(c:字节，w:双字，k:KB，M:MB，G:GB)
find / -size -1000k 　　#查找出小于1000KB的文件
find / -user fred -or -user george 　　#在/目录下查找用户是fred或者george的文件文件
find / -user fred -and -user george 　　#在/目录下查找用户是fred并且george的文件文件
find /tmp ! -user panda　　#在/tmp目录中查找所有不属于panda用户的文件
```
 
 
 