#### 兼容
```
chrome 43往上
Firefox 38往上
IE 6-11
MS Edge
Safari 5往上
```

#### 循环
```
<script type="text/javascript">
    console.log('------- javascript -------');
    //js原生的循环方法
    for(var i = 0; i < 5; i++){
        console.log(i);
    }
    console.log('------- lodash -------');
    //ladash的times方法
    _.times(5,function(a){
        console.log(a);
    });
</script>
```

#### 遍历属性
```
// a simple array
var arr = [1,2,3,4,5];
 
// array.map will set each element to what is returned
// and I can use the value of each element in the process.
arr = arr.map(function(el){
 
    return el * 10;
 
});
 
console.log(arr);
// [10,20,30,40,50]

//lodash
var arr = [1,2,3,4,5];
 
arr = _.map(arr, function(el){
 
    return el * 10;
 
});
 
console.log(arr);
// [10,20,30,40,50]

var obj = {foo: 'bar', anwser: 42};
 
console.log(_.map(obj, function(item){
 
    return item;
 
}));
// ['bar',42]
```

#### 深克隆
```
<script type="text/javascript">
    var objA = {
        "name": "戈德斯文"
    };
    var objB = _.cloneDeep(objA);
    console.log(objA);
    console.log(objB);
    console.log(objA === objB);
</script>
```

#### 指定范围获取随机值
```
<script type="text/javascript">
    function getRandomNumber(min, max){
        return Math.floor(Math.random() * (max - min)) + min;
    }
    console.log(getRandomNumber(15, 20));

    console.log(_.random(15, 20));

</script>
```

#### 对象扩展
```
<script type="text/javascript">
    Object.prototype.extend = function(obj) {
        for (var i in obj) {
            if (obj.hasOwnProperty(i)) {    //判断被扩展的对象有没有某个属性，
                this[i] = obj[i];
            }
        }
    };

    var objA = {"name": "戈德斯文", "car": "宝马"};
    var objB = {"name": "柴硕", "loveEat": true};

    objA.extend(objB);
    console.log(objA); 

    console.log(_.assign(objA, objB));
</script>
```
`_.assign` 方法也可以接收多个参数对象进行扩展，都是往后面的对象上合并


#### 去重
```
<script type="text/javascript">
    var arr1 = [2, 1, 2];

    var arr2 = _.uniq(arr1);


    function unique(arr) {
        var newArr = [];
        for (var i = 0; i < arr.length; i++) {
            if(newArr.indexOf(arr[i]) == -1){
                newArr.push(arr[i]);
            }
        }
        return newArr;
    }

    console.log(arr1);
    console.log(arr2);
    console.log(unique(arr1));
</script>
```

其他参看[lodash中文文档地址](http://www.css88.com/doc/lodash/)