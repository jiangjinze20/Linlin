javascript核心知识
====

##### 01.请写出弹出值,并解释为什么?  梳理js体系 词法作用域

```javascript
alert(a);
a();
var a = 3;

function a() {
	alert(10);
}
alert(a);
a = 6;
a();

function a() {
alert(10);
}
var a;
alert(a);
a();

a = 3;
alert(a);
a = 6;
a();
//函数体->10->3->a is not a function
1.函数提升在变量提升之前
2.函数名与变量名重名
function test(){
	   console.log(1);
  } 
  var test = 2 ; //不管定义在函数前后 输出都是2 
  var test;//undefined 会被忽略,输出函数 没有意思 如果赋值undefined是有意义的 
  console.log(test)//2
  
  扩展:
	 (1).函数提升
	 test(); // 1
	 function test(){
	    console.log(1);
	 }
	 (2).变量提升
	 if(false){
	    var a = 1;
	}
	console.log(a);//undefined
	var a //变量提升
	if(false){
		a = 1;
	}
	(3).表达式函数声明,命名的函数只能在内部使用且不能被重写
	var test = function test(){
	   console.log(1);
	}
	//console.log(test);//函数体

	(function test(){
	   表达式声明的函数只能在内部访问
	})();
	test() ;//is not defined
	var q = function test(){ //test函数只能在内部使用并且不能被重写
		test = 1;
		console.log('1',typeof test)//function
		console.log(test);
	}
	q();
	console.log(test);
	(4).函数私有作用域
	//函数里面私有作用域		
	function test(){
		var a =1 ;
	}
	test();
	alert(a);//a is not defined
		
	      
```

##### 02.请写出如下输出值

```javascript
//构造函数的优先级大于原型链  new 会指向new的对象
//箭头函数会改变this的指向 箭头函数的this会固定它的父级[箭头函数的this是它爹的this]
this.a = 20;
var test = {
	a: 40,
	init: function() {
	  console.log(this.a);
	}
     }

test.init(); //40

this.a = 20;
var test = {
	a: 40,
	init: () => {
	     console.log(this.a);
	}
     }

test.init(); //20	

简单扩展:this指向window
this.a = 20;
function test(){
   console.log(this.a);
}
test();//20  windows.test()
```
##### 03.bind
```javascript
1.硬绑
this.a = 20;
function test(){
	console.log(this.a);
}
var obj = {
	a : 30
}

var result = test.bind(obj);
result();//30 硬绑

2.软绑
this.a = 20;
function test(){
	console.log(this.a);
}
var obj = {
	a : 30
}

var result = test.bind(null);
result();//20软绑 不想this改变[不想被硬绑]
		
3.new会让bind失效

var o = {
foo : function(){
    console.log('哈哈');
},
bar(){
   console.log(this); //o
   console.log('嘿嘿');
  }
}

o.bar();

var f = o.foo.bind({});
new f();

var p = o.bar.bind({});//p是函数
new p(); //Uncaught TypeError: p is not a constructor  es6bind是不能new的

4.self是全局变量不要轻易赋值
//许多变量时这么判断的self.self == self //true 你改了就不等了
```

##### 3.1 bind的原理实现
```javascript
 1.前端测试
<script src="./bindnew.js" type="text/javascript" charset="utf-8"></script>	
<script type="text/javascript">
function test(data1,data2){
	console.log(data1);
	console.log(data2);
}

test.prototype.yideng = function(){
	console.log('测试函数');
}

var obj = {
	a:30
}

var result = test.bind(obj,'京程');
//result('一灯');
var ins = new result('一灯');
ins.yideng();

2.完整版
//es-shim
//原来的函数 apply this 的值
//http://www.cnblogs.com/happypayne/p/7739514.html Array.prototype.slice.call()方法的理解
//https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind polyfill官方地址
//https://blog.csdn.net/u010552788/article/details/50850453 bind的博客实现

if (!Function.prototype.bind) (function(){  //不跟原生的bind产生冲突
	Function.prototype.bind = function(oThis){
	if(typeof this !== 'function'){
		throw new TypeError('请使用函数执行')
	}
	var aArgs = Array.prototype.slice.call(arguments,1), //第一个参数是oThis 外面的参数
		fToBind  = this, //保存原有的this  原来的函数
		fNOP    = function() {},//后面用
		fBound   = function(){ //返回的值
			return  fToBind.apply(this instanceof fBound ? this : oThis,aArgs.concat(Array.prototype.slice.call(arguments))); //apply es3 Array.prototype.slice.call(arguments) 外部执行函数的值
		}
	if(this.prototype){
		fNOP.prototype = this.prototype;
	}
	fBound.prototype = new fNOP();
	return fBound;  //为什么要返回函数 因为它本来就是得到一个函数在我们在执行
	}
})();

3.简易版
Function.prototype.bind =  function(target){
var self = this;
return function(args){
	if(!(args instanceof Array)){
		args = [args];
	}
	self.apply(target, args)
   }
}



</script>
```

##### 5.
```javascript
function C1(name) {     
		if (name) this.name = name;	
	} 
	function C2(name) {     this.name = name; } 
	function C3(name) {     this.name = name || 'fe'; } 
	C1.prototype.name = "yideng"; 
	C2.prototype.name = "lao";
	C3.prototype.name = "yuan"; 
	console.log((new C1().name) + (new C2().name) + (new C3().name));

//一灯 	undefined    fe		
```
##### 6.this的增强
```javascript
1.
var list_li = document.getElementsByTagName("li");
	 for (var i = 0; i < list_li.length; i++) {
	 list_li[i].onclick = function() {
	 console.log(i);
 }
 2.
var list_li = document.getElementsByTagName("li");
	 for (var i = 0; i < list_li.length; i++) {
	 list_li[i].onclick = function() {
	 console.log(this.innerHTML);
 }
 3.
 var list_li = document.getElementsByTagName("li");
	 for (let i = 0; i < list_li.length; i++) {
	 list_li[i].onclick = function() {
	 console.log(i+1);
 }
 4.闭包
 
 5.块级作用域扩展
  (1).
  块级作用域的扩展
     {
	console.log(1); // 1
     }
  (2).{} + []  // 0   隐式转换
  (3).console.log({} + []) //[object Object]  括号充当了表达式 {} 被当成表达式 [object Object]  + ''
  (4).小object 和大Object的区别   ?
	  typeof {} "object"
	  大Object是类型  小object是为了区分是 Object 表示出来的值  一种字符串的表示形式
	  typeof 实例返回的字符串的表示形式
  	
```
##### 7.坑人题
```javascript
function yideng() {
    console.log(1);
}
(function () {
	// var yideng;
	 if (false) {
	 function yideng() {
	 console.log(2);
	 }
}
 yideng();
})()

答案:
  1.最早时间  1
  2.中间  2
  3.现在  yideng is not a function

```
##### 8.智商题
```javascript
//请用一句话算出0-100之间学生的学生等级，如90-100输出为1等生、80-90为2等
//以此类推。不允许使用if switch等。   扩展性   写代码要聪明
function grade(x){
    return 10-(x/10);
}	
```
##### 9.一句话遍历
```javascript
请用一句话遍历变量a。(禁止用for 已知var a = "abc")
var a = 'abc';
console.log(Array.from(a));
console.log([...new Set(a)]);
console.log(Array.prototype.slice.call(a,0));
```
##### 10.
```javascript
//var length = 10; 注释这个 1  2 
function fn() { 
   console.log(this.length);  //this.length 页面iframne 的数量
} 
var yideng = { 
   length: 5, 
   method: function(fn) { 
   fn(); 
   arguments[0](); //arguments 的数量  arguments.fn()
   } 
}; 
yideng.method(fn, 1);
// 10   2 

```
##### 10.写出输出值，并解释为什么
```
function test(m) {
 m = {v:5}//m.v=5
}
var m = {k: 30};
test(m);
alert(m.v);//undefined

 // 值传递
  var a = 1;
  var b = a;
  b = 3;
  alert(a);
  alert(b);

  //按引用地址传递  
  var a = {qq : 25};
  var b = a;
  b.xx = 1;
  console.log(a);
  console.log(b);

   b={xx:111}->重写
  一定要区分 按引用传递 / 重写

  var a = {aa : 66};
	var b = a;
	b = {aa:99}
	//	两次的输出结果
	{aa: 66}
	{aa: 99}

	b.aa = 99
	//	两次的输出结果
	{aa: 99}
	{aa: 99}	


```
