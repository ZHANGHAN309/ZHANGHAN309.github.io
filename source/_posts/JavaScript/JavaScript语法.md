---
title: JavaScript语法
date: 2025/11/12 8:43:00
tags: 
    - JavaScript
    - 语法
categories: 技术篇
---

# 基础

## 基础类型和运算逻辑

首先说明JavaScript注释与C是一样的，JS语句后可以不加`;`，但是可能会出现预料之外的错误。

基础类型包括64位双精度double，布尔true/false，字符串`'ABC'`/`"ABC"`，非数字类型的数字：Infinity(1/0)的结果，NaN(0/0)的结果。

基础运算包括

```JavaScript
1 + 1; // = 2
0.1 + 0.2; // = 0.30000000000000004
8 - 1; // = 7
10 * 2; // = 20
35 / 5; // = 7
5 / 2; // = 2.5

1 << 2; // = 4

!true; // = false
!false; // = true

1 === 1; // = true
2 === 1; // = false

1 !== 1; // = false
2 !== 1; // = true

1 < 10; // = true
1 > 2; // = false
1 <= 10; // = true
1 >= 2; // = false

'Hello' + ' world'; // = Hello world
"a" < "b"; // = true
"5" == 5; // = true
null == undefined; // = true
"5" === 5; // = false
null === undefined; // = false
13 + !0; // = 14
"13" + !0; // = "13true"
```

## 变量、数组和对象

```JavaScript
var some = 5;
// 如果没加var关键字，也不会出现错误，但是这个变量的作用域会变成全局
secsome = 10;

var unde; // = undefined

// 变量可以使用+= -= ++ --运算符
some += 5;
some -= 5;
some++;
some--;

// 数组可以是任意类型组成的有序列表
var myArray = ["Hello",15,true];
myArray[1]; // = 15

// 数组也有方法可调用
myArray.push("World");

// JS对象相当于其他语言的字典或映射
var myObj = {myKey:"Say","Another:4};
myObj["Another"]; // = 4
```

## 逻辑控制结构

```JavaScript
//if语句同C
var a = 5;
if(a == 1)
{
    // a == 1
}
else if(a == 2)
{
    // a == 2
}
else
{
    // 其他
}

// while循环
while(a)
{
    // 一直循环
}

// do-while
do
{
    // 循环
}while(a)

// for同C
for(var i = 0; i < a; i++)
{
    // 循环
}

// && 和 ||
if(a < 1 || a > 5)
{
    // 执行
}

// && 和 ||是短路语句，在设置初始值时特别有用
var name = otherName || "default"; // otherName为真时，赋值otherName；otherName为假时，赋值default
var name = otherName && "default"; // otherName为真时，赋值default；otherName为假时，赋值otherName

// switch
switch(a)
{
    case 1:
        console.log("1");
        break;
    case 2:
        console.log("2");
        break;
    default:
        break;
}
```

## 函数、作用域、闭包
```JavaScript

// JavaScript 函数由`function`关键字定义
function myFunction(thing){
    return thing.toUpperCase();
}
myFunction("foo"); // = "FOO"

// 函数可以作为对象赋值给变量，相当于C++中的回调函数
setTimeout(myFunction, 5000);

// 函数也可以不用声明名称，直接定义
setTimeout(function(){}, 5000);

// 在函数外部声明的变量和函数是全局作用域，未使用var,let,const的变量，默认为全局变量
// 浏览器环境中，全局变量默认挂载到window对象上，Node.js挂载到global对象上
// 函数作用域：函数内部声明的变量只在函数内部有效，var,let,const均受限制
// 块级作用域：{}内部声明的变量只在块内有效，let,const受限制，var不受限制
// 其他块级结构，包括块语句、try...catch、switch 以及其中一个 for 语句的头部，对于 var 并不创建作用域，而在这样的块内部使用 var 声明的变量仍然可以在块外部被引用。

const globalVar = "我是全局变量";
function fun1()
{
    console.log(globalVar);
    var a = 1; // 函数作用域变量
}
console.log(a); // Error

{
    let b = 2; // 块级作用域变量
}
console.log(b); // Error

// JavaScript最强大的功能之一就是闭包。
// 如果一个函数在另一个函数中定义，那么这个内部函数就拥有外部函数的所有变量的访问权，
// 即使在外部函数结束之后。
function sayHelloInFiveSeconds(name){
    var prompt = "Hello, " + name + "!";
    // 内部函数默认是放在局部作用域的，
    // 就像是用`var`声明的。
    function inner(){
        alert(prompt);
    }
    setTimeout(inner, 5000);
    // setTimeout是异步的，所以 sayHelloInFiveSeconds 函数会立即退出，
    // 而 setTimeout 会在后面调用inner
    // 然而，由于inner是由sayHelloInFiveSeconds“闭合包含”的，
    // 所以inner在其最终被调用时仍然能够访问`prompt`变量。
}
sayHelloInFiveSeconds("Adam"); // 会在5秒后弹出 "Hello, Adam!"
```

变量提升是指变量声明在代码中位于变量使用后，运行时却优先于脚本执行之前处理，具体可见 
{$ post_link JavaScript/变量提升 "变量提升\n" $}

## 对象、构造函数和原型

```JavaScript
// 对象可以包含函数，函数可以访问对象的参数，对象的成员函数可以赋值给变量，但是如果对象失效的话，这个变量就会运行失败;
// 当然也可以给对象的成员函数赋值
var myObj = {
    var myString = "Hello World!";
    myFunc: function()
    {
        return this.myString;
    }
}
var anotherFunc = myObj.myFunc;
anotherFunc();
myObj.myFunc = function()
{
    return this.myString.toUpperCase();
}

// 当通过'call'和'apply'调用函数的时候，可以为其指定一个上下文，唯一的区别是apply要求传递列表
anotherFunc = function(s)
{
    return this.myString + s;
}
anotherFunc.call(myObj, "Ni Hao");
anothreFunc.apply(myObj, ["Ni Hao"]);

// 如果想要将函数和对象绑定，可以使用bind
var boundFunc = anotherFunc.bind(myObj);
boundFunc("Ni Hao");

// `bind` 也可以用来部分应用一个函数（柯里化）
// 柯里化是指分步传递参数
var product = function(a, b){ return a * b; }
var doubler = product.bind(this, 2);
doubler(8); // = 16

// 当你通过`new`关键字调用一个函数时，就会创建一个对象，
// 而且可以通过this关键字访问该函数。
// 设计为这样调用的函数就叫做构造函数。
var MyConstructor = function(){
    this.myNumber = 5;
}
myNewObj = new MyConstructor(); // = {myNumber: 5}
myNewObj.myNumber; // = 5

// 原型__proto__有点类似对象的继承，或者是关联
// A的原型是B，那么A就能访问B的成员变量和函数，当B的成员变量被修改时，A访问的值也会跟着变化

var myObj = {
    myString: "Hello World!";
}
var myPrototype = {
    meaningOfLife: 42,
    myFunc: function(){
        return this.myString.toLowerCase()
    }
};

myObj.__proto__ = myPrototype;
myObj.meaningOfLife; // = 42
myObj.myFunc(); // = hello world!
myPrototype.meaningOfLife = 66;
myObj.meaningOfLife; // = 66

// 原型之间的关系会形成一条原型链，如果原型没有这个属性，就会向原型的原型进行访问，直到访问到null

// 有两种方式指定原型
// 1.Object.create 这种方式并不支持所有JS版本
var myObj = Object.create(myPrototype);
myObj.meaningOfLife; // = 66
// 2.通过构造函数
MyConstructor.prototype = {
    number: 5,
    getNumber: function()
    {
        return this.number;
    }
};
var myNewObj = new MyConstructor();
myNewObj.getNumber(); // = 5
myNewObj.myNumber = 6;
myNewObj.getNumber(); // = 6
```

**原型核心用法**
```JavaScript
// 原型的核心用法
// 1.共享方法/属性，节省内存
function Student(name) {
  this.name = name;
}

// 所有 Student 实例共享 study 方法
Student.prototype.study = function() {
  console.log(`${this.name} is studying`);
};

const s1 = new Student("Bob");
const s2 = new Student("Charlie");

s1.study(); // "Bob is studying"
s2.study(); // "Charlie is studying"

// 验证方法是共享的（同一引用）
console.log(s1.study === s2.study); // true

// 2.实现基础
// 父类构造函数
function Animal(type) {
  this.type = type;
}
Animal.prototype.eat = function() {
  console.log(`${this.type} is eating`);
};

// 子类构造函数
function Dog(name) {
  this.name = name;
}

// 关键：让子类原型指向父类实例，实现继承
Dog.prototype = new Animal("dog");
// 修复子类原型的 constructor 指向（否则会指向 Animal）
Dog.prototype.constructor = Dog;

// 子类新增方法
Dog.prototype.bark = function() {
  console.log(`${this.name} is barking`);
};

// 测试
const dog1 = new Dog("Buddy");
dog1.eat(); // "dog is eating"（继承自 Animal 原型）
dog1.bark(); // "Buddy is barking"（子类自身原型方法）

// 拓展内置对象(谨慎使用)
// 为 Array 扩展一个求和方法
Array.prototype.sum = function() {
  return this.reduce((total, item) => total + item, 0);
};

const nums = [1, 2, 3];
console.log(nums.sum()); // 6
```

# 参考

十分推荐以下网站
[Y分钟速成X](https://learnxinyminutes.com/zh-cn/javascript/)：包含了大量编程技术，可以在短时间速成
