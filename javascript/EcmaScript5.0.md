EcmaScript5.0  
======


##### 进入严格模式之后，行为变更：
`https://www.zhangxinxu.com/wordpress/2012/01/introducing-ecmascript-5-1/ 张鑫旭的日记`
    1.全局变量声明时，必须加关键字(var)
        正常模式：a = 10;    console.log(a)    //10
        严格模式：a = 10;    console.log(a)    //a is not defined
    2.this无法指向全局对象
        正常模式：function fn(){ console.log(this) }        //window
        严格模式：function fn(){ console.log(this) }        //undefined
    3.函数内不允许出现重名参数
        正常模式：function fn( a,b,b ){ console.log(a,b) }
                fn(1,2,3)        //1,3
        严格模式：function fn( a,b,b ){ }
        //报错：Duplicate parameter name not allowed in this context    在此上下文中不允许出现重复的参数名
    4.arguments对象
        4.1 arguments对象不允许被动态改变
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
        4.2 arguments对象不允许被自调用（递归）
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
    5.新增的保留字：implements，interface，let，package，private，protected，public，static，yield
