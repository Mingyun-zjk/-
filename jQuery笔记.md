## jQuery笔记

### jquery 特点

1. 如果报了错误：$ is not defined , 就是说明没有引入jQuery文件

``` html
        #(function () {

        });
```

2. jQuery文件结构其实是自执行函数

``` html
        (function (){
        window.jQuery = window.$ = jQuery;
        }())
```

3. > a. 引入一个js文件,是会执行js文件中的代码的

   > b. jQuery文件是一个自执行函数, 执行这个jQuery文件中的代码, 其实就是执行这个自执行函数

   > c. 这个自执行函数就是给window对象添加一个jQuery属性和$属性

   > d. $和jQuery是等价的, 是一个函数

   > e. 如果传递的是一个字符串 $("#one") 是一个选择器

   >这是创建一个div


``` js
        $("<div>嘀嘀嘀</div>")
```

### dom对象与jQuery对象之间的相互转化

1. jQuery对象可以转为dom对象，

    例1：(使用下标来取出来)
    var $divs = $("div");
    var div1 = $divs[0];
    sonsole.log(div1);
    例2：(使用jQuery方法 .get())
    var div2 = $divs.get(1);
    console.log(div2);

2. 同样dom对象也可以转为jQuery对象,

    例如：(加钱$)
    var div1 = document.getElementById("one");
    var $div1 = $(div1);
    console.log($div1);

dom对象 : 原生js选择器获取到的对象

特点 : 只能调用dom方法或者属性, 不能够调用jQuery的方法和属性

``` js
    document.getElementById();
    document.getElementsByTagName();
    例如:
    html 代码: <div id="one"></div>
    js 代码: var div1 = document.getElementById("one");
    div1.style.backgroundColor = "red";
    是正确的
    div1.css("backgroundColor", "red");
    是错误的, 报错: div1.css is not a function 因为dom对象不能够调用jQuery对象的方法
```
jQuery对象 : 利用jQuery选择器获取到的对象
特点 :

    1.只能调用jQuery方法或者属性,不能够调用原生js的方法和属性

    2. jquery对象是一个伪数组,jQuery对象其实就是一个dom对象的包装集

``` js
    例如:
        html 代码: <div id="one"></div>
    js 代码: var $div1 = $("one");
    $div1.css("backgroundColor", "red");
    是正确的, jQuery对象是可以调用jQuery对象的方法的.
    $div1.style.backgroundColor = "red";
    是错误的, 报错: Cannot set property 'backgroundColor' of undefined;
```

``` js
    例如:
    <div></div>
    <div></div>
    <div></div>
    var divs = $("div"); //其实divs就是上述三个div的集合
```


### jquery 当中的过滤选择器

1. eq选择器，index 从 0 开始

    - $("div:eq(2)").css("backgroundColor","red");

2. odd 偶数选择器

    - $("div:even").css("backgroundColor","red");

3. 奇数选择器

    - $("div:odd").css("backgroundColor","red");

### jQuery当中的筛选选择器(方法)


| 名称                 | 用法                          | 描述                         |
| ------------------ | --------------------------- | :------------------------- |
| children(selector) | $('ul').children('li')      | 相当于$('ul-li')，子类选择器        |
| find(selector)     | $('ul').find('li');         | 相当于$('ul li'),后代选择器        |
| siblings(selector) | $('#first').siblings('li'); | 查找兄弟节点，不包括自己本身。            |
| parent()           | $('#first').parent();       | 查找父亲                       |
| eq(index)          | $('li').eq(2);              | 相当于$('li:eq(2)'),index从0开始 |
| next()             | $('li').next()              | 找下一个兄弟                     |
| prev()             | $('li').prev()              | 找上一次兄弟                     |



### jQuery当中的方法

#### text() 设置和获取文本

1. 获取文本 ： .text() 没有参数

    - 会获取到这个标签当中的所有文本，包括后代元素中的文本。

    - 包含了多个dom元素的jQuery对象，通过text()获取文本，会把所有dom元素的文本获取到。

2. 设置文本 ： .text(参数)  参数就是要设置的文本

    - 如果此元素还有后代元素，那么设置.text()方法会覆盖它原来的内容

    - 如果设置的文本中包含了标签，那么text()方法是不会把这个标签解析出来的。如：$(".div1").text("新设置的文本\<a>我是一个超链接\</a>");

    - 包含了多个dom元素的jQuery对象，通过text()方法设置文本，会把所有的dom元素都设置上。如：$(".div").text("新设置的文本");

#### css() 设置和获取样式

1. 获取样式 ：css()方法设置参数为要获取值得样式名

    - 如： $('.div1").css("backgroundColor");

    - 在IE浏览器下如果要获取像border这样的样式值，一定要记得要给一个准确的边框,$(".div1").css("border-top-width");

    - 获取包含了多个dom元素的jQuery对象的样式值，只能获取到第一个dom对象的样式值。

2. 设置样式 ： .css("属性名","属性值");

    - 设置的样式是行内样式

    - 另一种方法设置多样式 .css({"属性名":"属性值", ...}

#### addClass() 添加类

1. 使用方法： 元素.addClass("类名")

2. 给元素添加一个类名或多个类名

    - 添加一个类名 如： $(".div1").addClass("fontSize30")

    

    - 给元素添加多个类名 $(".div1").addClass("fontSize30 bgcRed")

#### removeClass() 移除类

1. 使用方法： 元素.removeClass("类名")

2. 给元素移除一个类名或多个类名或者全部类名

    - 移除一个类名 如： $(".div1").removeClass("fontSize30")

    

    - 给元素移除多个类名 $(".div1").removeClass("fontSize30 bgcRed")

    - 移除全部的类名 $(".div1").removeClass()

#### .hasClass() 判断类

1. 使用方法： 元素.hasClass("类名"), 判断一个元素有没有某个类名，如果有则返回true，没有则返回false

#### .toggleClass() 切换类

1. 使用方法： 元素.toggleClass("类名"), 如果元素有某个类就移除这个类，如果元素没有这个类就添加这个类




### jQuery动画

#### show(参数1，参数2) 显示

1. 可以没有参数，修改的是行内样式 display：block；

    例如：

    - 给元素移除多个类名 $(".div1").removeClass("fontSize30 bgcRed")

``` js
        $(".div1").show() //这个方法没有参数，那就没有动画效果
```

2. 可以有参数

    - 参数1 ：代表执行动画的时长 毫秒数， 也可以是代表时长的字符串 fast normal slow

    例如：

``` js
    $(".div1").show(2000) //2秒内显示结束
    $(".div1").show('fast') // 200毫秒
    $('.div1').show('normal') // 400毫秒
    $('.div1').show('slow') // 600毫秒
    $('.div1').show('solw') // 如果参数写错了，那么默认为normal
```
    - 参数2 ：代表动画执行完毕后的回调函数
``` js
    $('.div1').show(2000, function() {
        alter("动画执行完毕了");
    })
```

#### .hide(参数1，参数2) 隐藏（大致内容同show()）

1. $(".div1").hide() 没有参数没有动画效果

2. $(".div1").hide(2000) 2秒内隐藏

3. $(".div1").hide("fast",function(){alert("隐藏了");})

#### toggle(参数1，参数2) 切换（show()与hide()的切换）

1. 如果元素隐藏状态就显示；如果元素显示状态就隐藏
    - 给元素移除多个类名 $(".div1").removeClass("fontSize30 bgcRed")

``` js
    $(".BtnToggle").click(function() {
        $('.div1').toggle(200); // 当然也可以加回调函数
    })
```

#### slideDown(参数1，参数2) 滑入

1. 参数1： 动画执行的时长

2. 参数2： 动画的回调函数

* 没有参数 如：$(".div1").slideDown(), 则默认给了一个时长，normal代表400毫秒

#### slideup(参数1，参数2) 滑出 

#### slideToggle(参数1，参数2) 切换（滑入与滑出之间的切换）

1. 元素是隐藏状态就滑入；元素是显示状态就滑出

#### fadeIn(参数1，参数2) 淡入

* 改变的是透明度，使用方法同上

* 参数1是时长，参数2是回调函数

#### fadeOut(参数1，参数2) 淡出

#### fadeToggle(参数1，参数2) 淡入与淡出之间的切换

#### fadeTo(时长，透明度) 淡入到哪里

* 指定一个透明度 

#### animate() 自定义动画

* 参数1：必选的  对象(可以写多个)   代表的是需要做动画的属性

* 参数2：可选的  代表执行动画的时长

* 参数3: 可选的  取值为 swing(先满后快然后再慢) 或者 linear(匀速), 默认为swing

* 参数4： 可选的  动画执行完毕后的回调函数

``` js
    $(".div1").animate({
        left: 800,
        width: 300,
        oopacity: 0.5
    }, 2000, 'swing', function() {
        alert("动画执行完毕了");
    })

    //既然参数4是一个回调函数，那么就可以一直使用回调函数来执行一堆的代码，比如说继续调用自定义函数
    $(".div1").animate({
        left: 800,
        width: 300,
        oopacity: 0.5
    }, 2000, 'swing', function() {
        $(".div1").animate({
            top: 300,
            height: 300,
            oopacity: 1
        }, 2000, 'swing', function() {
            alert("动画执行完毕了");
        })
    })
```

#### 动画队列与停止动画（防止发生鬼畜）

* 在同一个元素上执行多个动画，那么对于这个动画来说，后面的动画会被投放到动画队列当中，等前面的动画执行完毕后，才会执行（下拉列表slideDown(), 会发生鬼畜）（联想火车进站）

1. stop(参数1，参数2) 方法： 停止动画效果

    - 参数1 ： 是否清除队列  取值为 true/false

    - 参数2 ： 是否跳转到最终结果 取值为 true/false

    - 如果stop()不写参数，默认为两个false,false,

    - [教学视频（黑马程序员）](https://www.bilibili.com/video/BV1pt411H7D6?p=30 )

    - 解决下拉列表的方法

$mdFormatter$38$mdFormatter$

``` js
        详细请看： 下拉列表.html
        $(".menu > li").mouseover(function() {
            $(this).children(".submenu").stop(true, false).slideDown(300);
        })
        $(".menu > li").mouseout(function() {
            $(this).children(".submenu").stop(true, false).slideUp(150);
        })

        或者直接使用.stop()

        $(".menu > li").mouseover(function() {
            $(this).children(".submenu").stop().slideDown(300);
        })
        $(".menu > li").mouseout(function() {
            $(this).children(".submenu").stop().slideUp(150);
        })
```

筛选选择器的功能与过滤选择器有点类似，但是用法不一样，筛选选择器主要是方法

1. .children() 子类选择器

    - $('ul').children('li') 相当于 $('ul > li'), 子类选择器

2. .find() 后代选择器

    - $('ul').find('li') 相当于 $('ul li'), 后代选择器

3. .siblings() 兄弟选择器

    - $('#first').siblings('li') 查找兄弟节点，不包括自身

4. .parent()

    - $('#first').parent() 查找父亲

5. .eq()

    - $('li').eq(2) 相当于 $('li:eq(2)'), index 从0开始

6. .next()

    - $('li').next(); 找下一个兄弟

7. .prev()

    - $('li').prev(); 找上一个兄弟

### 动态创建元素

1. 原生js中创建节点： 
    - document.write('\<div>abc\</div>'),会解析出元素。 脚下留心：慎用，有可能会覆盖页面

    - innerHTML()

    - document.createElement('div');

2. jQuery 中创建节点

    * html() 设置或者获取内容

        获取内容： html() 方法不给参数。获取到元素的所有内容，包括标签

        设置内容：html() 方法给参数。会把原来的内容给覆盖。如果设置的内容中包含标签，会把标签给解析出来的          
         
    - $()

        确实可以创建元素，但是创建的元素只存在于内存中，如果要在页面上显示，需要追加。需要使用.append($div)来把这个新的元素添加到页面结构里面去。
### 随手小记

    - jquery 当中的.show()方法其实就是更改display属性的值为block；.hide()方法则把display属性的值更改为none

    - jQuery 的鼠标移入事件是.mouseover(),在鼠标移动到选取的元素及其子元素上时触发;.mouseenter()事件只在鼠标移动到选取的元素上时触发。以后如果有使用鼠标移入事件就是用.mouseenter()事件

    - jquery 移出事件是.mouseout()和.mouseleave(),而在开发中则使用.mouseleave()

    - css方法有返回值，返回值就是使用这个方法元素本身，通常 $(this).css().siblings()

    - jquery特性：饮食迭代

    - jQuery特性：链式编程，在于一个方法返回的是一个就jQuery对象，既然是jQuery对象那么就可以继续点出jQuery方法来。

    - .index() 方法获取当前元素的索引值。 **注意：表示的是这个元素在其他兄弟元素间的排行** 

    * 例题如下：
``` html
    <li><a href=""><img src="img/jpg" alt=""></a></li>
    <li><a href=""><img src="img/jpg" alt=""></a></li>
    <li><a href=""><img src="img/jpg" alt=""></a></li>
    <li><a href=""><img src="img/jpg" alt=""></a></li>
```

    * 思考题： 为什么要给li元素设置鼠标的移入事件，而不是给a标签设置鼠标的移入事件？

    * 因为给a标签设置的话不会拿到正确的索引值，a标签是它自己本身的老大，下标永远都是0；但是给li设置鼠标移入事件就不一样，li有其他兄弟元素li，所以.index()的值会改变。




