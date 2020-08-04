【作用域】

# 作用域定义

- JS作用域：代码名字（变量）在某个范围内起作用和效果
- 目的：提高程序的可靠性，减少命名冲突
- 分类（ES6之前）：全局作用域，局部作用域
  - 全局作用域：整个script标签，或者是一个单独的js文件
  - 局部作用域：函数内部，这个代码的名字只在函数内部起作用


# 变量的作用域

根据作用域分类：

- 全局变量：在全局作用域下的变量

```html
<script>
	var num = 10;
	console.log(num); // num是全局变量

	function fn() {
		console.log(num); // 这里的num也是全局变量

		num2 = 20; // !!!在函数内部，没有声明直接赋值的变量也属于全局变量 
	}
</script>
```

- 局部变量：在局部作用域下的变量(函数内部的变量)

```html
<script>
	function fun(aru) {    //函数的形参也是局部变量
		var num1 = 10;
	}

	fun();
	console.log(num1); //num1 为局部变量，在全局下未定义，会报错

	// 从执行效率来看
	// 全局变量，只在浏览器关闭时才会销毁，比较占用内存资源
	// 局部变量，当程序执行完毕时就会销毁，比较节约内存资源
</script>
```

## JS没有块级作用域

ES6 之后新增了块级作用域

块级作用域：用花括号{}包含的 if{} for{}


# 作用域链

```html
<script>
	// 只要是代码，就至少有一个作用域
	// 写在函数内部的是局部作用域
	// 如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域
	// 根据“内部函数可以访问外部函数变量”的机制，用链式查找能决定哪些数据能被内部函数访问，这就成为作用域链

	var num = 10;
	function fn() {
		var num = 20;
		function fun() {
			console.log(num); //这里的num输出为20（就近原则）
			//作用域链：内部函数访问外部函数的变量，采取的是链式查找的方式来决定取哪个值，这种结构称为作用域链（就近原则）
		}
	}
</script>
```

## 作用域链案例

案例1：
```html
<script>
	function f1() {
		var num = 123;
		function f2() {
			console.log(num); //站在目标出发，一层一层往外查找
		}
		f2();
	}
	var num = 456;
	f1();     //结果输出为123
</script>
```

案例2：

```html
<script>
	var a = 1;
	function fn1() {
		var a = 2;
		var b = '22';
		fn2();
		function fn2() {
			var a = 3;
			fn3();
			function fn3() {
				var a = 4;
				console.log(a);  //a为4
				console.log(b);  //b为22
			}
		}
	}
	fn1();
</script>
```