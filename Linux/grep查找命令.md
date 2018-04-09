##### 文件夹递归查找
`$ grep -r "192.168.1.5" /etc/`   或   `$ grep -R "192.168.1.5" /etc/`

输出：
![](http://p6.qhimg.com/t01d022a1352fbd1f9b.png)

可以禁止文件路径输出：
`$ grep -hR "192.168.1.5" /etc/`
![](http://p9.qhimg.com/t0120b09e2f75fe1794.png)


##### 文本查找
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
 
 
 