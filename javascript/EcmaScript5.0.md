EcmaScript5.0  
======

##### 1.严格模式的作用：

    1.消除了JS语法的一些不合理、不严谨之处，减少一些怪异行为；
    2.消除代码运行的一些不安全之处，保证代码运行的安全；
    3.提高编译器效率，增加运行速度；
    4.为未来新版本的JS做好铺垫

    严格模式体现了JS更合理，更安全，更严谨的发展方向，包括IE10在内的主流浏览器都已经支持它了

    注意：同样的代码，在“严格模式”中，可能会有不一样的运行结果，一些在“正常模式”下可以正常运行的语句，在“严格模式”下将不能运行，掌握这些内容，有助于更细致深入的理解JS，让你编程一个更好的程序员。



##### 2.进入严格模式之后，行为变更：

https://www.zhangxinxu.com/wordpress/2012/01/introducing-ecmascript-5-1张鑫旭的日记 
* 将过失错误转成异常

``` javascript
    1.无法意外创建全局变量:
        全局变量声明时，必须加关键字(var)
        正常模式：a = 10;    console.log(a)    //10
        严格模式：a = 10;    console.log(a)    //a is not defined
```   
``` javascript
    2.严格模式会使引起静默失败
    静默失败 : 不报错也没有任何效果的赋值操作抛出异常
        "use strict";
        // 给不可写属性赋值
        var obj1 = {};
        Object.defineProperty(obj1, "x", { value: 42, writable: false });
        obj1.x = 9; // 抛出TypeError错误
        // 给只读属性赋值
        var obj2 = { get x() { return 17; } };
        obj2.x = 5; // 抛出TypeError错误
        // 给不可扩展对象的新属性赋值
        var fixed = {};
        Object.preventExtensions(fixed);
        fixed.newProp = "ohai"; // 抛出TypeError错误
```
``` javascript
    3.严格模式重名属性被认为语法错误
      "use strict";
       var o = { p: 1, p: 2 }; // !!! 语法错误
```
``` javascript
    4.函数内不允许出现重名参数[参数名唯一]
        正常模式：function fn( a,b,b ){ console.log(a,b) }
                fn(1,2,3)        //1,3
        严格模式：function fn( a,b,b ){ }
        //报错：Duplicate parameter name not allowed in this context    在此上下文中不允许出现重复的参数名
```
```javascript
   5.严格模式禁止八进制数字语法
       "use strict";
        var sum = 015 + // !!! 语法错误
        正常模式
        var a = 0o10; // ES6: 八进制

```


* 简化变量的使用
 
``` javascript
    1.严格模式下eval 函数内部声明的变量不能再函数外部使用。
    "use strict";
    eval("var a = 10");
    a= 15;
    console.log(a);//语法错误
```
``` javascript
    2.禁用with,使用with会引起语法错误--推荐的替代方案是声明一个临时变量来承载你所需要的属性。
      with延长作用域链,降低性能   
      https://blog.csdn.net/zwkkkk1/article/details/79725934
       var obj = {
            a: 1,
            b: 2,
            c: 3
        };
        // 重复写了3次的“obj”
        obj.a = 2;
        obj.b = 3;
        obj.c = 4;
            
        with (obj) {
            a = 3;
            b = 4;
            c = 5;
        }
``` 
``` javascript
    3.严格模式禁止删除声明变量。delete name 在严格模式下会引起语法错误：
    "use strict";
    var x;
    delete x; // !!! 语法错误
    eval("var y; delete y;"); // !!! 语法错误
```
* arguments变的简单

``` javascript  
    1.arguments对象不允许被动态改变
            正常模式：function fn(a){
                        a=20;
                        console.log(a);                //20
                        console.log(arguments[0]);     //20
                    }
                    fn(10);
            严格模式：function fn(a){
                        a=20;
                        console.log(a);                //20
                        console.log(arguments[0]);     //10
                    }
                    fn(10);
     2. arguments对象不允许被自调用（递归）
            正常模式：function fn(a){
                        if( a == 1 ){
                            return 1;
                        }
                        return arguments.callee(a-1) + a;
                    }
                    fn(3);            //6
            严格模式：function fn(a){
                        if( a == 1 ){
                            return 1;
                        }
                        return arguments.callee(a-1) + a;
                    }
                    //报错：'caller', 'callee', and 'arguments' properties may
           not be accessed on strict mode functions or the arguments objects for calls to them
                    //报错："caller"，"arguments"，"callee"，不能在严格模式下使用
```
* 安全的javascript

``` javascript
    this无法指向全局对象
        正常模式：function fn(){ console.log(this) }        //window
        严格模式：function fn(){ console.log(this) }        //undefined
 ```

* 为未来的javascript铺路

      新增的保留字：implements，interface，let，package，private，protected，public，static，yield
