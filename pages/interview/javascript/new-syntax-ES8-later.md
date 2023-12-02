## ES12 - logical assignment operators

**逻辑赋值运算符**(logical assignment operators)是 ES12 新增的特性，可以简化逻辑赋值语句。

```javascript
message ||= "默认值";	// message = message || "默认值"
message ??= "默认值";	// message = message ?? "默认值"
obj && obj.running && obj.running()	// 逻辑与一般应用场景
```

>  逻辑或赋值运算符比较常见，主要应用在变量值不存在时设置默认值，逻辑与赋值运算符应用场景较少。

***

## ES12 - replaceAll

**replaceAll()** 会将匹配到的字符串全部替换，返回一个新的结果。

```javascript
const message = "my name is sun ,sun is 18";

const newMessage = message.replace("sun", "hou");	// "my name is hou ,sun is 18"
const newMessage2 = message.replace("sun", "hou");	// "my name is hou ,hou is 18"
```

***

## ES13 - method.at()

**method.at()** 可以接收一个可以为负数的索引值。

```javascript
const names = ['sun', 'hou', 'ting'];

console.log(names.at(1));	// 'hou'
console.log(names.at(-1));	// 'ting'

const str = 'Hello sunnng';

console.log(str.at(1));	// 'e'
console.log(str.at(-1));	// 'g'
```

***

## ES13 - Object.hasOwn(obj,propKey)

Object 中新增了一个静态方法（类方法）：**Object.hasOwn(obj, propKey)**，该方法用于判断**一个对象中是否有某个自己的属性**，旨在替代 **obj.hasOwnProperty()**。

```javascript
const obj = {
  name: "sunnng",
  age: 18,
  __proto__: {
    address: "shanghai"
  }
}

Object.hasOwn(obj, name)	// true
Object.hasOwn(obj, address)	// false
```

***

## ES13 - class 中新的成员

+ instance public fields：公共实例属性（公共对象属性）
+ static public fields：静态公共属性（公共类属性）
+ instance private fields：私有实例属性（私有对象属性）
+ static private fields：静态私有属性（私有类属性）
+ static block：静态代码块

```javascript
class Person {
	height = 1.88;	// 公共的实例字段
  #address = 'china';	// # 开头的对象属性是一个私有属性，只有在类的内部才能访问
  static totalCount = 10; // static 修饰的是一个类属性
  static #maleCount = 5; // 私有的类属性
  
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

	// 静态代码块：类第一次被加载时执行，且只会执行一次
	static {
    console.log("Hello world!");
  }
}

const p = new Person("sunnng", 18);
console.log(p.height);	// 1.88
console.log(p.#address);	// error 无法访问
console.log(Person.totalCount)	// 10
console.log(Person.#maleCount)	// error 无法访问
```

