javascript核心知识
====

#### 01.请写出弹出值,并解释为什么?  梳理js体系 词法作用域

```javascript
  	alert(a); 
		a();
		var a = 3;
		function a(){
			alert(10);
		}
		alert(a);
		a=6;
		a();
    
    function a(){
			alert(10);
		}
		var a ;
		alert(a); 
		a();
		
		a = 3;
		alert(a);
		a=6;
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
    
    
	      
```
