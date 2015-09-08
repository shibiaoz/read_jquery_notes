- jquery 总体结构
- 自调用匿名函数
- 为什么传入参数window
- 为什么传入参数undefined
- 自调用匿名函数前后的分号的作用


> jquery 总体结构

```
    (function(window, undefined){
        var jQuery = (function () {
            var jQuery = function () {
                ...
            }
            return jQuery;
        })()
        //
        //工具模块
        //选择器模块
        //...
        window.jQuery = window.$ = jQuery;
    })(window);
```

> 自调用匿名函数

- 作用是创造一个特殊的作用域，所有的变量只是在当前作用域有效，对外可认为是私有变量
- 不会污染全局变量，同时也不会受其他框架或库的影响
- 常见写法
```
    // way-1
    （function(){

    }）();

    //way-2
    (function(){}());

    // way-3 特殊符号强制座位表达式执行
    !function(){}();
    +function(){}();
    ~function(){}();

```

> 为什么传入参数window

传入参数window，window作为实参，即局部变量
js的作用域是基于原型链查找的，不必回退到顶层作用域
能更快的访问

> 为什么传入参数undefined

- 减少原型链查找，更快访问
- 保证参数undefined是真的undefined

```
    alert('undefined' in window) ;// true
    undefined是window的一个特殊的属性
    另外undefined可以被重写
    undefined = 'not really undefined';// 有浏览器兼容问题

```


> 自调用匿名函数前后的分号的作用

```
    // 两个demo 如果不见分号（）容易被当成函数的执行
    var a = 1
    (function(){})()
    // 1 is not a function

    (function(){alert(1)})()
    (function(){alert(2)})()
    // 第一个正确执行，然后报错 (intermediate value)(...) is not a function
```



