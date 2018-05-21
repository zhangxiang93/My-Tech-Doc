## 收集那些Javascript函数段子

#### 千分位逗号格式化数字
一行代码解决(正则：从后往前数每三个数字加一个逗号)
```
function toThousands(num) {
    return (num || 0).toString().replace(/(\d)(?=(?:\d{3})+$)/g, '$1,');
}
```