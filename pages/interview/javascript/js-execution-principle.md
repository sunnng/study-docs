# Javascript执行原理

## 全局代码的执行过程

### 1. 初始化全局对象（Global Object）

js 引擎在**执行代码之前**，会在**堆内存中创建一个全局对象**：Global Object(GO)

+ 该对象在**所有作用域**（scope）中都可以访问；
+ 里面会包含Date、Array、String、Number、setTimeout、setInterval等等；
+ 其中还会有一个**window属性**指向自己。

```javascript
console.log(message, num1, num2)	// undefined,undefined,undefined

var message = "Global Message";

function foo() {
	var message = "Foo Message";
}

var num1 = 10;
var num2 = 20;
var result = num1 + num2;

console.log(result)
```

### 2. 执行上下文（Execution Contexts）

JS 引擎内部有一个执行上下文栈（Execution Context Stack，ECS），它是用于执行代码的调用栈。

初始化全局对象后，JS引擎会构建一个全局执行上下文（Global Execution Context，GEC）。GEC 会被放入 ECS 中，具体会执行两项工作： 

+ 代码执行前，执行上下文都会关联一个VO（Variable Object，变量对象），**全局定义的变量和函数声明**会先被解析为机器可执行的语言并添加到VO中（执行全局代码时，VO 就是 GO），变量和函数此时已经存在，但是值为 undefined（函数先于变量被声明）。

![image-20231203002511836](./assets/image-20231203002511836.png)

+ 在代码执行的过程中，会对变量进行赋值，或者执行其他的函数。

![image-20231203002937694](./assets/image-20231203002937694.png)

## 函数代码的执行过程

以下面的代码为例：

```javascript
console.log(message, num1, num2)	// undefined,undefined,undefined

var message = "Global Message";

function foo(num) {
	var message = "Foo Message";
  console.log(message)
}

foo(123);

var num1 = 10;
var num2 = 20;
var result = num1 + num2;

console.log(result);
```

### 1. 创建执行上下文

在执行过程中遇到函数调用时，会根据函数体创建一个**函数执行上下文**（Function Execution Context，FCS），并且压入ECS中。

**因为每个执行上下文都会关联一个VO，那么函数执行上下文关联的VO是什么呢？**

+ 当函数执行上下文进栈时，会创建一个**AO对象**（Activation Object）；
+ 这个 AO 对象会使用**arguments 进行初始化**，并且**初始值是传入函数的参数**；
+ 这个 AO 对象会作为执行上下文的 VO 来存放变量的初始化。

![image-20231203005213174](./assets/image-20231203005213174.png)

## 2. 执行代码

![image-20231203005339920](./assets/image-20231203005339920.png)