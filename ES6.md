#### ES6笔记

##### const 与 let

var : 重复声明，不能限制修改，函数级
let ：不能重复声明，变量，块级{}
const： 不能重复声明，常量，块级{}

##### 解构赋值

1. 两边的结构必须一样
- let {a,b} = [12,4]  //  错 
2. 右边必须是个东西
- let {a,b} = {12,4} // 错
3. 解构和赋值同时完成
- let {a,b};
 {a,b} = {a:12,b:4} // 错
4. 正确的案例
- arr = [11,23,22]
 let [a,b,c] = arr

##### 箭头函数

1. 可以简写了
() => {}

简写注意事项：
-  如果有且仅有一个参数，()可以不写
-  如果有且仅有一个语句并且是return，{}也可以不写

2. 修正this
this从一出生就已经绑定了

##### ...

1. 参数展开
- 收集参数
    ```js
        function show(a,b,...c){
            console.log(a,b,c);
        }
        show(123,4,1,3,21,23);

        // 如果是以下方式，则发生错误
        function show(a,b,...c,d){  // ...c 只能是在最后一位
            console.log(a,b,c,d);
        }
        show(123,4,1,3,21,23);
    ```
2. 数组展开
    
    ```js
        let arr = [12,4,8];
        function show(a,b,c){
            return (a+b+c);
        }
        show(arr) // 错误的，默认把arr数组传递给了a
        show(...arr)    // 正确的，默认把数组arr展开，成为了12，4，8
    ```
    小例子，实现数组的合并
    ```js
        let arr1 = [11,22,33];
        let arr2 = [44,55,66];
        console.log(...arr1,...arr2); // 11,22,33,44,55,66
    ```

3. json展开
    ```js
        let json = {a:12,b:5,c:99};
        let json1 = {
            ...json,
            d: 99
        }
    ```

##### array 扩展

###### map  (映射，一一对应) [12,89,43] -->[不及格，及格，不及格]

```js
    let arr = [65,53,12,98,65];
    let arr1 = arr.map(function (item)[
        if(item>= 60){
            return '及格';
        }else{
            return '不及格';
        }
    ]);
    console.log(arr); // [65, 53, 12, 98, 65]
    console.log(arr1); //  ["及格", "不及格", "不及格", "及格", "及格"]
```
另外一种箭头函数的方式
```js
    let arr = [65, 53, 12, 98, 65];
    let arr1 = arr.map(item => item >= 60 ? '及格':'不及格');
    console.log(arr); // [65, 53, 12, 98, 65]
    console.log(arr1); //  ["及格", "不及格", "不及格", "及格", "及格"]
```

###### reduce (缩减，不管进去多少个出来一定是一个 n>=1)

求平均数
```js
    let arr = [68, 53, 12, 98, 65];
    let result = arr.reduce(function (temp, item, index) {
        if (index == arr.length -1) {
            return (temp + item) / arr.length;
        } else {
            return temp + item;
        }
    })
    console.log(result);
```

###### filter 过滤

小例子：取出偶数
```js
    let arr = [68, 53, 12, 98, 65,44,43];
    let result = arr.filter(item => item % 2 == 0);
    console.log(result); // [68, 12, 98, 44]
```

###### forEach 遍历，循环走一遍

```js
    let arr = [68, 53, 12, 98, 65,44,43];
    arr.forEach((item,index) => {
        console.log(`第${index}个：${item}`)
    })
    // 第0个：68
    // 第1个：53
    // 第2个：12
    // 第3个：98
    // 第4个：65
    // 第5个：44
    // 第6个：43
```

        

##### json 对象

 ```js
    let json = {a: 10 ,b: 32};
    let json1 = JSON.stringify(json);
    console.log(json1); //{"a":10,"b":32}
```
json 有它自己的规范，详情去百度
```js
    let str = '{"a" : 10 ,"b": 32}';
    let json = JSON.parse(str);
    console.log(json); // {a: 10, b: 32, name: "hehe"}
```

##### 异步操作 

ajax('http://taobao.com/api/aa.html',function () {});

异步操作：同时进行多个操作，用户体验好，代码混乱
同步操作：一次只能进行一个操作，用户体验差，代码清晰

###### 融合异步、同步

Promise
async/await

Promise -- 对异步操作的统一封装

###### 面向对象

ES5: 1. 面向对象--> 假的 2. 没有统一的写法
- ES5写法
```js
    // 以函数形式来写对象
    function Person(name,age){
        this.name = name;
        this.age = age;
    }
    // 添加方法
    Person.prototype.showName = function () {
        alert(this.name);
    }
    Person.prototype.showAge = function () {
        alert(this.age);
    }
    let person1 = new Person("blue",19);
    person1.showName();
    person1.showAge();
```

- ES6写法
```js
    // 有单独的类的声明和构造函数的声明
    class Person{
        constructor(name,age){
            this.name = name; 
            this.age = age;
        }
        showName () {
            alert(this.name);
        }
        showAge(){
            alert(this.age);
        }
    }
    let person2 = new Person("mingyun", 12);
    person2.showName();
    person2.showAge();
```
- 继承
> class     类声明
> extends   继承
> constructor 构造函数
> super  父类/超类

1. 省事
2. 便于扩展

ES5当中的写法
```js
    
    function Person(name, age) {
        this.name = name;
        this.age = age;
    }
    // 添加方法
    Person.prototype.showName = function () {
        alert(this.name);
    }
    Person.prototype.showAge = function () {
        alert(this.age);
    }

    function Worker(name,age,job){
        Person.call(this,name,age); //完成父类属性的继承
        this.job = job;
    }

    Worker.prototype = new Person();
    Worker.prototype.constructor = Worker;
    Worker.prototype.showJob = function () {
        alert(this.job);
    }

    let worker1 = new Worker("mingyun",12,"老师");
    worker1.showName();
    worker1.showAge();
    worker1.showJob();
```
ES6当中的写法
```js
    class Person {
        constructor(name, age) {
            this.name = name;
            this.age = age;
        }
        showName() {
            alert(this.name);
        }
        showAge() {
            alert(this.age);
        }
    }
    class Worker extends Person{
        constructor(name,age,job){
            super(name,age);
            this.job = job;
        }
        showJob(){
            alert(this.job);
        }
    }

    let worker2 = new Worker("mingyun", 12, "老师");
    worker2.showName();
    worker2.showAge();
    worker2.showJob();
```

###### 模块系统

ES6模块语言支持，浏览器不支持，如果要使用，需要编译，通过webpack，
1. 定义
2. 使用

###### ES7

幂操作
> 原来的方法求：Math.pow(3,5)
> 现在的方法求：alert(3**5)
Array.includes()
> let arr = [1,2,3,4,5]
> alert(arr.includes(8))  // false

###### webpack

安装： npm install webpack-cli -g


###### node模块使用

1. 新建文件夹node_demo,在此文件夹内打开命令行工具，将此文件夹初始化为node(npm)的项目执行`npm init -y`,此时该文件夹里多了package.json文件
2. 新建index.html 页面
3. 安装jQuery插件，执行 `npm install jquery`,执行完毕后，文件夹内多了很多的文件
    - node_modules 文件夹，该文件夹是用来存储下载好的包
    - package-lock.json 该文件是记录安装包的详细信息
4. 在html中使用jQuery，可以按照之前的路径引用（不推荐），现在是使用npm下载的模块，可以使用node模块的方式导入安装好的包. 使用`require ('包名')`
5. 但是当模块导入之后，浏览器不支持，因为模块语法浏览器不支持，需要使用webpack来编译

###### node模块语法

前端模块分为： 核心模块，第三方模块，自定义模块
模块的导入： require('包名')，前两种模块直接写包名，自定义模块写路径
模块的导出： module.exports = {值}

npm使用：
npm就是下载 node 包的工具
下载方式有一下三种：
> `npm i 包名 --save`   这种方法一般下载的是项目的必须包,记录到package.json的dependencies字段内
    ```js
        npm install jquery@2.3.4 --save
        npm i jquery -S
        npm i jquery
        //这三仲方式是一样的
    ```
> `npm i 包名 包名 --save-dev`, 这种方式安装的是项目的非必须包（工具类）,记录到package.json的devDependencies字段内
    ```js
        npm install webpack --save-dev
        npm i webpack -D
    ```
> `npm i -g 包名` 这种方式是全局安装，当你想要在你的电脑上任何地方都是用包的时候进行全局安装
    ```js
        npm i -g server
    ```
卸载包使用：
> `npm uninstall 包` 通过哪种方式安装的就通过哪种方式卸载

npm 下载包的好处：
- 可以使用模块导入
- 下载的包的信息全部记录到package.json 内
- 同事之间互相传递项目的时候不需要传递node_modules文件夹。需要使用的时候只需要执行`npm i`命令会重新将所有的包下载一遍

npmd的技巧：
- 切换npm包的来源，默认是从外网，有点慢
    ```
        npm config set registry http://registry.npm.taobao.org
    ```
- 加上http显示配置，不让等待的过程无聊
    ```
        npm config set loglevel=http
    ```

###### 使用webpack打包编译我们的项目

你的node项目内使用node模块导入的各种包，webpack可以实现将模块的导入导出编译成为浏览器所认识的语法，也可以将所有的导入模块打包。

如何使用[参考链接](https://www.webpackjs.com/guides/)

1. 项目内安装webpack
```
    npm install webpack webpack-cli --save-dev
```
2. 将项目内的js文件夹重命名为src，保证项目的根目录下有src文件夹，并且src文件夹下存在index.js,并且index.js是页面主要的js文件
3. 执行编译打包命令`npx webpack`,会将index.js打包编译到项目下的dist文件夹内的main.js
4. 页面导入打包好的js

###### 
