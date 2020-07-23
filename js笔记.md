# JavaScript 笔记

## Object.prototype.toString.call()

### 使用Object.prototype上的原生toString()方法判断数据类型，使用方法如下

Object.prototype.toString.call(value)

1. 判断基本类型

> Object.prototype.toString.call(null); //”[object Null]”
> Object.prototype.toString.call(undefined); //”[object > Undefined]”
> Object.prototype.toString.call(“abc”); //”[object String]”
> Object.prototype.toString.call(123); //”[object Number]”
> Object.prototype.toString.call(true); //”[object Boolean]”

2. 判断原生引用类型

> - 函数类型
> Function fn(){console.log(“test”); }
> Object.prototype.toString.call(fn); //”[object Function]”
> - 日期类型
> var date = new Date(); 
> Object.prototype.toString.call(date); //”[object Date]”
> - 数组类型
> var arr = [1, 2, 3]; 
> Object.prototype.toString.call(arr); //”[object Array]”
> - 正则表达式
> var reg = /[hbc]at/gi; 
> Object.prototype.toString.call(arr); //”[object RegExp]”
> - 自定义类型
>

``` js
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
```

>
> var person = new Person("Rose", 18); 
> Object.prototype.toString.call(person); //”[object Object]”

很明显这种方法不能准确判断person是Person类的实例，而只能用instanceof 操作符来进行判断，如下所示：
console.log(person instanceof Person); //输出结果为true

3. 判断原生JSON对象：

> var isNativeJSON = window. JSON && Object.prototype.toString.call(JSON); 
> console.log(isNativeJSON); //输出结果为”[object JSON]”说明JSON是原生的，否则不是

``` js
__proto__ 是每个对象都有的属性
```

``` js
    < script >

        function a(xx) {
            this.x = xx;
            return this;
        }

    var x = a(5);
    var y = a(6);
    console.log(x.x); //undefined  解析：x.x也就是6.6，x作为number类型的属性(包装类),不报错，返回undefined
    console.log(y.x); //6 解析：y.x也就是window.x,打印6

    例如：
    var xx = 1;
    var yy = 2;
    console.log(xx.yy); //undefined 解析： 1.2，同上，返回undefined
    <
    /script>
```
