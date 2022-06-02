<!--
 * @Author: hidari
 * @Date: 2022-05-23 10:37:10
 * @LastEditors: hidari 
 * @LastEditTime: 2022-06-02 09:29:59
 * @FilePath: \deepJavaScript\README.md
 * @Description: 深入JavaScript
 * 
 * Copyright (c) 2022 by 1640106564@qq.com, All Rights Reserved. 
-->
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [深入JavaScript](#%E6%B7%B1%E5%85%A5javascript)
  - [深入JavaScript运行原理](#%E6%B7%B1%E5%85%A5javascript%E8%BF%90%E8%A1%8C%E5%8E%9F%E7%90%86)
    - [浏览器工作原理](#%E6%B5%8F%E8%A7%88%E5%99%A8%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86)
    - [JavaScript引擎](#javascript%E5%BC%95%E6%93%8E)
    - [JavaScript的执行过程](#javascript%E7%9A%84%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B)
    - [JS执行函数的方法](#js%E6%89%A7%E8%A1%8C%E5%87%BD%E6%95%B0%E7%9A%84%E6%96%B9%E6%B3%95)
    - [变量环境和记录](#%E5%8F%98%E9%87%8F%E7%8E%AF%E5%A2%83%E5%92%8C%E8%AE%B0%E5%BD%95)
    - [作用域提升面试题](#%E4%BD%9C%E7%94%A8%E5%9F%9F%E6%8F%90%E5%8D%87%E9%9D%A2%E8%AF%95%E9%A2%98)
  - [JS的内存管理和闭包](#js%E7%9A%84%E5%86%85%E5%AD%98%E7%AE%A1%E7%90%86%E5%92%8C%E9%97%AD%E5%8C%85)
    - [认识内存管理](#%E8%AE%A4%E8%AF%86%E5%86%85%E5%AD%98%E7%AE%A1%E7%90%86)
      - [JS的内存管理](#js%E7%9A%84%E5%86%85%E5%AD%98%E7%AE%A1%E7%90%86)
    - [JS的垃圾回收](#js%E7%9A%84%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6)
      - [常见的GC算法 – 引用计数](#%E5%B8%B8%E8%A7%81%E7%9A%84gc%E7%AE%97%E6%B3%95--%E5%BC%95%E7%94%A8%E8%AE%A1%E6%95%B0)
      - [常见的GC算法 – 标记清除](#%E5%B8%B8%E8%A7%81%E7%9A%84gc%E7%AE%97%E6%B3%95--%E6%A0%87%E8%AE%B0%E6%B8%85%E9%99%A4)
    - [闭包](#%E9%97%AD%E5%8C%85)
      - [JS中函数是一等公民](#js%E4%B8%AD%E5%87%BD%E6%95%B0%E6%98%AF%E4%B8%80%E7%AD%89%E5%85%AC%E6%B0%91)
      - [JS中闭包的定义](#js%E4%B8%AD%E9%97%AD%E5%8C%85%E7%9A%84%E5%AE%9A%E4%B9%89)
      - [闭包的访问过程](#%E9%97%AD%E5%8C%85%E7%9A%84%E8%AE%BF%E9%97%AE%E8%BF%87%E7%A8%8B)
      - [闭包的执行过程](#%E9%97%AD%E5%8C%85%E7%9A%84%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B)
      - [闭包的内存泄露](#%E9%97%AD%E5%8C%85%E7%9A%84%E5%86%85%E5%AD%98%E6%B3%84%E9%9C%B2)
      - [AO不使用的属性](#ao%E4%B8%8D%E4%BD%BF%E7%94%A8%E7%9A%84%E5%B1%9E%E6%80%A7)
  - [JS函数的this指向](#js%E5%87%BD%E6%95%B0%E7%9A%84this%E6%8C%87%E5%90%91)
    - [this指向](#this%E6%8C%87%E5%90%91)
      - [规则一：默认绑定](#%E8%A7%84%E5%88%99%E4%B8%80%E9%BB%98%E8%AE%A4%E7%BB%91%E5%AE%9A)
      - [规则二：隐式绑定](#%E8%A7%84%E5%88%99%E4%BA%8C%E9%9A%90%E5%BC%8F%E7%BB%91%E5%AE%9A)
      - [规则三：显示绑定](#%E8%A7%84%E5%88%99%E4%B8%89%E6%98%BE%E7%A4%BA%E7%BB%91%E5%AE%9A)
        - [call、apply、bind](#callapplybind)
        - [内置函数的绑定思考](#%E5%86%85%E7%BD%AE%E5%87%BD%E6%95%B0%E7%9A%84%E7%BB%91%E5%AE%9A%E6%80%9D%E8%80%83)
      - [规则四：显示绑定](#%E8%A7%84%E5%88%99%E5%9B%9B%E6%98%BE%E7%A4%BA%E7%BB%91%E5%AE%9A)
      - [规则优先级](#%E8%A7%84%E5%88%99%E4%BC%98%E5%85%88%E7%BA%A7)
      - [this规则之外 – 忽略显示绑定](#this%E8%A7%84%E5%88%99%E4%B9%8B%E5%A4%96--%E5%BF%BD%E7%95%A5%E6%98%BE%E7%A4%BA%E7%BB%91%E5%AE%9A)
      - [this规则之外 - 间接函数引用](#this%E8%A7%84%E5%88%99%E4%B9%8B%E5%A4%96---%E9%97%B4%E6%8E%A5%E5%87%BD%E6%95%B0%E5%BC%95%E7%94%A8)
      - [this规则之外 – ES6箭头函数](#this%E8%A7%84%E5%88%99%E4%B9%8B%E5%A4%96--es6%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0)
      - [面试题](#%E9%9D%A2%E8%AF%95%E9%A2%98)
  - [JS函数式编程](#js%E5%87%BD%E6%95%B0%E5%BC%8F%E7%BC%96%E7%A8%8B)
    - [实现apply、call、bind](#%E5%AE%9E%E7%8E%B0applycallbind)
    - [call](#call)
      - [apply](#apply)
      - [bind](#bind)
      - [arguments](#arguments)
      - [箭头函数不绑定arguments](#%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0%E4%B8%8D%E7%BB%91%E5%AE%9Aarguments)
    - [JavaScript纯函数](#javascript%E7%BA%AF%E5%87%BD%E6%95%B0)
      - [纯函数的案例](#%E7%BA%AF%E5%87%BD%E6%95%B0%E7%9A%84%E6%A1%88%E4%BE%8B)
      - [纯函数的优势](#%E7%BA%AF%E5%87%BD%E6%95%B0%E7%9A%84%E4%BC%98%E5%8A%BF)
    - [JavaScript柯里化](#javascript%E6%9F%AF%E9%87%8C%E5%8C%96)
      - [柯里化的结构](#%E6%9F%AF%E9%87%8C%E5%8C%96%E7%9A%84%E7%BB%93%E6%9E%84)
      - [柯里化作用](#%E6%9F%AF%E9%87%8C%E5%8C%96%E4%BD%9C%E7%94%A8)
      - [自动柯里化函数](#%E8%87%AA%E5%8A%A8%E6%9F%AF%E9%87%8C%E5%8C%96%E5%87%BD%E6%95%B0)
    - [组合函数](#%E7%BB%84%E5%90%88%E5%87%BD%E6%95%B0)
  - [JS额外知识补充](#js%E9%A2%9D%E5%A4%96%E7%9F%A5%E8%AF%86%E8%A1%A5%E5%85%85)
    - [with语句](#with%E8%AF%AD%E5%8F%A5)
    - [eval函数](#eval%E5%87%BD%E6%95%B0)
    - [严格模式](#%E4%B8%A5%E6%A0%BC%E6%A8%A1%E5%BC%8F)
  - [JS面向对象](#js%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1)
    - [对属性操作的控制](#%E5%AF%B9%E5%B1%9E%E6%80%A7%E6%93%8D%E4%BD%9C%E7%9A%84%E6%8E%A7%E5%88%B6)
      - [数据属性描述符](#%E6%95%B0%E6%8D%AE%E5%B1%9E%E6%80%A7%E6%8F%8F%E8%BF%B0%E7%AC%A6)
      - [存取属性描述符](#%E5%AD%98%E5%8F%96%E5%B1%9E%E6%80%A7%E6%8F%8F%E8%BF%B0%E7%AC%A6)
      - [同时定义多个属性](#%E5%90%8C%E6%97%B6%E5%AE%9A%E4%B9%89%E5%A4%9A%E4%B8%AA%E5%B1%9E%E6%80%A7)
      - [对象方法补充](#%E5%AF%B9%E8%B1%A1%E6%96%B9%E6%B3%95%E8%A1%A5%E5%85%85)
    - [创建多个对象的方案](#%E5%88%9B%E5%BB%BA%E5%A4%9A%E4%B8%AA%E5%AF%B9%E8%B1%A1%E7%9A%84%E6%96%B9%E6%A1%88)
      - [工厂模式](#%E5%B7%A5%E5%8E%82%E6%A8%A1%E5%BC%8F)
      - [构造函数](#%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)
      - [对象的原型](#%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%8E%9F%E5%9E%8B)
      - [函数的原型 prototype](#%E5%87%BD%E6%95%B0%E7%9A%84%E5%8E%9F%E5%9E%8B-prototype)
      - [重写原型对象](#%E9%87%8D%E5%86%99%E5%8E%9F%E5%9E%8B%E5%AF%B9%E8%B1%A1)
    - [面向对象的特性 – 继承](#%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%89%B9%E6%80%A7--%E7%BB%A7%E6%89%BF)
      - [JavaScript原型链](#javascript%E5%8E%9F%E5%9E%8B%E9%93%BE)
      - [通过原型链实现继承](#%E9%80%9A%E8%BF%87%E5%8E%9F%E5%9E%8B%E9%93%BE%E5%AE%9E%E7%8E%B0%E7%BB%A7%E6%89%BF)
      - [借用构造函数继承](#%E5%80%9F%E7%94%A8%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0%E7%BB%A7%E6%89%BF)
      - [原型式继承函数](#%E5%8E%9F%E5%9E%8B%E5%BC%8F%E7%BB%A7%E6%89%BF%E5%87%BD%E6%95%B0)
      - [寄生式继承函数](#%E5%AF%84%E7%94%9F%E5%BC%8F%E7%BB%A7%E6%89%BF%E5%87%BD%E6%95%B0)
      - [寄生组合式继承](#%E5%AF%84%E7%94%9F%E7%BB%84%E5%90%88%E5%BC%8F%E7%BB%A7%E6%89%BF)
      - [对象的方法补充](#%E5%AF%B9%E8%B1%A1%E7%9A%84%E6%96%B9%E6%B3%95%E8%A1%A5%E5%85%85)
      - [原型继承关系](#%E5%8E%9F%E5%9E%8B%E7%BB%A7%E6%89%BF%E5%85%B3%E7%B3%BB)
    - [类](#%E7%B1%BB)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


# 深入JavaScript

## 深入JavaScript运行原理

### 浏览器工作原理

1. 不同的浏览器有不同的内核组成
    1. `Gecko`：早期被Netscape和Mozilla Firefox浏览器浏览器使用；
    2. `Trident`：微软开发，被IE4~IE11浏览器使用，但是Edge浏览器已经转向Blink；
    3. `Webkit`：苹果基于KHTML开发、开源的，用于Safari，Google Chrome之前也在使用；
    4. `Blink`：是Webkit的一个分支，Google开发，目前应用于Google Chrome、Edge、Opera等；

2. 浏览器内核指的是浏览器的排版引擎

3. HTML解析的时候遇到了JavaScript标签，会停止解析HTML，而去加载和执行JavaScript代码

![浏览器渲染过程](/image/01/%E6%B5%8F%E8%A7%88%E5%99%A8%E6%B8%B2%E6%9F%93%E8%BF%87%E7%A8%8B.png)

### JavaScript引擎

1. 为什么需要JavaScript引擎呢？
    - 我们前面说过，高级的编程语言都是需要转成最终的机器指令来执行的
    - 事实上我们编写的JavaScript无论你交给浏览器或者Node执行，最后都是需要被CPU执行的
    - 但是CPU只认识自己的指令集，实际上是机器语言，才能被CPU所执行
    - 所以我们需要JavaScript引擎帮助我们将JavaScript代码翻译成CPU指令来执行

2. 浏览器内核和JS引擎的关系

这里我们先以WebKit为例，WebKit事实上由两部分组成的
- `WebCore`：负责HTML解析、布局、渲染等等相关的工作
- `JavaScriptCore`：解析、执行JavaScript代码

3. V8引擎的原理

V8是用C ++编写的Google开源高性能JavaScript和WebAssembly引擎，它用于Chrome和Node.js等，可以独立运行，也可以嵌入到任何C++应用程序中。

![v8引擎原理](/image/01/v8%E5%BC%95%E6%93%8E%E5%8E%9F%E7%90%86.png)

1. `Parse`模块会将JavaScript代码转换成`AST（抽象语法树）`，这是因为解释器并不直接认识JavaScript代码
    - 如果函数没有被调用，那么是不会被转换成AST的
    - `Parse`的V8官方文档：https://v8.dev/blog/scanner
2. `Ignition`是一个解释器，会将`AST`转换成`ByteCode（字节码）`
    - 同时会收集`TurboFan`优化所需要的信息（比如函数参数的类型信息，有了类型才能进行真实的运算）
    - 如果函数只调用一次，`Ignition`会执行解释执行`ByteCode`
    - `Ignition`的V8官方文档：https://v8.dev/blog/ignition-interpreter
3. `TurboFan`是一个编译器，可以将字节码编译为CPU可以直接执行的机器码
    - 如果一个函数被多次调用，那么就会被标记为热点函数，那么就会经过`TurboFan`转换成优化的机器码，提高代码的执行性能
    - 但是，机器码实际上也会被还原为`ByteCode`，这是因为如果后续执行函数的过程中，类型发生了变化（比如sum函数原来执行的是number类型，后来执行变成了string类型），之前优化的机器码并不能正确的处理运算，就会逆向的转换成字节码
    - `TurboFan`的V8官方文档：https://v8.dev/blog/turbofan-jit


4. V8执行的细节
Blink将源码交给V8引擎，Stream获取到源码并且进行编码转换；
- `Scanner`会进行词法分析（lexical analysis），词法分析会将代码转换成tokens；
- 接下来`tokens`会被转换成AST树，经过`Parser`和`PreParser`：
    - `Parser`就是直接将tokens转成AST树架构；
    - `PreParser`称之为预解析，为什么需要预解析呢？
        - 这是因为并不是所有的JavaScript代码，在一开始时就会被执行。那么对所有的JavaScript代码进行解析，必然会影响网页的运行效率；
        - 所以V8引擎就实现了`Lazy Parsing（延迟解析）`的方案，它的作用是将不必要的函数进行预解析，也就是只解析暂时需要的内容，而对函数的全量解析是在函数被调用时才会进行；
        - 比如我们在一个函数outer内部定义了另外一个函数inner，那么inner函数就会进行预解析；
- 生成`AST树`后，会被`Ignition`转成`字节码（bytecode）`，之后的过程就是代码的执行过程

### JavaScript的执行过程

1. 初始化全局对象

js引擎会在执行代码之前，会在堆内存中创建一个全局对象：Global Object（GO）
- 该对象 所有的作用域（scope）都可以访问；
- 里面会包含Date、Array、String、Number、setTimeout、setInterval等等；
- 其中还有一个window属性指向自己

![堆内存](/image/01/%E5%A0%86%E5%86%85%E5%AD%98.png)

2. 执行上下文栈（调用栈）

js引擎内部有一个执行上下文栈（Execution Context Stack，简称ECS），它是用于执行代码的调用栈。
那么现在它要执行谁呢？执行的是全局的代码块：
 - 全局的代码块为了执行会构建一个 Global Execution Context（GEC）；
 - GEC会 被放入到ECS中 执行；
 - GEC被放入到ECS中里面包含两部分内容：
    - 第一部分：在代码执行前，在parser转成AST的过程中，会将全局定义的变量、函数等加入到GlobalObject中，但是并不会赋值；
        - 这个过程也称之为变量的作用域提升（hoisting）
    - 第二部分：在代码执行中，对变量赋值，或者执行其他的函数
![GEC被放入到ECS中](/image/01/GEC%E8%A2%AB%E6%94%BE%E5%85%A5%E5%88%B0ECS%E4%B8%AD.png)
![GEC开始执行代码](/image/01/GEC%E5%BC%80%E5%A7%8B%E6%89%A7%E8%A1%8C%E4%BB%A3%E7%A0%81.png)

### JS执行函数的方法

- 在执行的过程中执行到一个函数时，就会根据函数体创建一个`函数执行上下文（Functional Execution Context，简称FEC）`，并且压入到`EC Stack`中。
- `FEC`中包含三部分内容：
    - 第一部分：在解析函数成为`AST`树结构时，会创建一个`Activation Object（AO）`
        - `AO`中包含`形参`、`arguments`、`函数定义`和`指向函数对象`、`定义的变量`
    - 第二部分：作用域链：由`VO（在函数中就是AO对象）`和`父级VO`组成，查找时会一层层查找
    - 第三部分：`this`绑定的值
![函数执行上下文](/image/01/FEC.png)
![FEC被放入到ECS中](/image/01/FEC%E8%A2%AB%E6%94%BE%E5%85%A5%E5%88%B0ECS%E4%B8%AD.png)
![FEC开始执行代码](/image/01/FEC%E5%BC%80%E5%A7%8B%E6%89%A7%E8%A1%8C%E4%BB%A3%E7%A0%81.png)

### 变量环境和记录
1. 上面都是基于早期ECMA的版本规范：
![早期ECMA版本规范](/image/01/%E6%97%A9%E6%9C%9FECMA%E7%89%88%E6%9C%AC%E8%A7%84%E8%8C%83.png)
2. 在最新的ECMA的版本规范中，对于一些词汇进行了修改
![最新ECMA版本规范](/image/01/%E6%9C%80%E6%96%B0ECMA%E7%89%88%E6%9C%AC%E8%A7%84%E8%8C%83.png)

- 在最新的ECMA标准中，变量对象VO已经有另外一个称呼了变量环境VE

### 作用域提升面试题
```js
var n = 100
function foo() {
    n = 200
}
console.log(n) // 100
```
```js
function foo() {
    console.log(n) // undefined
    var n = 200
    console.log(n) // 200
}
var n = 100
foo()
```
```js
var n = 100
// 函数作用域链取决于定义的位置，而不是调用的位置
function foo1() {
    console.log(n) // 100
}
function foo2() {
    var n = 200
    console.log(n) // 200
    foo1()
}
foo2()
console.log(n) // 100
```
```js
var a = 100
function foo() {
    console.log(a) // undefined
    return // 在 return 前 变量已被定义
    var a = 100
}
foo()
```
```js
function foo() {
    var a = b = 100 // var a = 100; b = 100
}
foo()
// 全局作用域中找不到 a 
console.log(a) // a is not defined
console.log(b) // 100
```

## JS的内存管理和闭包

### 认识内存管理

- 不管什么样的编程语言，在代码的执行过程中都是需要给它分配内存的，不同的是某些编程语言需要我们自己手动的管理内存，某些编程语言会可以自动帮助我们管理内存：
- 不管以什么样的方式来管理内存，内存的管理都会有如下的生命周期：
    - 第一步：分配申请你需要的内存（申请）；
    - 第二步：使用分配的内存（存放一些东西，比如对象等）；
    - 第三步：不需要使用时，对其进行释放；
- 不同的编程语言对于第一步和第三步会有不同的实现：
    - 手动管理内存：比如C、C++，包括早期的OC，都是需要手动来管理内存的申请和释放的（`malloc`和`free`函数）
    - 自动管理内存：比如Java、JavaScript、Python、Swift、Dart等，它们有自动帮助我们管理内存；
- JavaScript通常情况下是不需要手动来管理的

#### JS的内存管理

JavaScript会在定义变量时为我们分配内存。
- JS对于`基本数据类型`内存的分配会在执行时，直接在栈空间进行分配；
- JS对于`复杂数据类型`内存的分配会在堆内存中开辟一块空间，并且将这块空间的指针返回值变量引用
![JS内存管理](/image/02/JS%E5%86%85%E5%AD%98%E7%AE%A1%E7%90%86.png)

### JS的垃圾回收
- 因为内存的大小是有限的，所以当内存不再需要的时候，我们需要对其进行释放，以便腾出更多的内存空间。
- 在手动管理内存的语言中，我们需要通过一些方式自己来释放不再需要的内存，比如`free`函数：
    - 但是这种管理的方式其实非常的低效，影响我们编写逻辑的代码的效率
    - 并且这种方式对开发者的要求也很高，并且一不小心就会产生内存泄露
- 所以大部分现代的编程语言都是有自己的垃圾回收机制：
    - 垃圾回收的英文是`Garbage Collection`，简称`GC`
    - 对于那些不再使用的对象，我们都称之为是垃圾，它需要被回收，以释放更多的内存空间
    - 而我们的语言运行环境，比如Java的运行环境JVM，JavaScript的运行环境js引擎都会内存 垃圾回收器
    - 垃圾回收器我们也会简称为`GC`，所以在很多地方你看到`GC`其实指的是垃圾回收器
- 但是这里又出现了另外一个很关键的问题：`GC`怎么知道哪些对象是不再使用的呢？
    - 这里就要用到GC的算法了

#### 常见的GC算法 – 引用计数
- 引用计数：
    - 当一个对象有一个引用指向它时，那么这个对象的引用就`+1`，当一个对象的引用为`0`时，这个对象就可以被销毁掉
- 这个算法有一个很大的弊端就是会产生循环引用
![GC算法-引用计数](/image/02/GC%E7%AE%97%E6%B3%95-%E5%BC%95%E7%94%A8%E8%AE%A1%E6%95%B0.png)

#### 常见的GC算法 – 标记清除
- 这个算法是设置一个`根对象（root object）`，垃圾回收器会定期从这个根开始，找所有从根开始有引用到的对象，对于哪些没有引用到的对象，就认为是不可用的对象
- 这个算法可以很好的解决循环引用的问题

- JS引擎比较广泛的采用的就是标记清除算法，当然类似于V8引擎为了进行更好的优化，它在算法的实现细节上也会结合一些其他的算法
![GC算法-标记清除](/image/02/GC%E7%AE%97%E6%B3%95-%E6%A0%87%E8%AE%B0%E6%B8%85%E9%99%A4.png)

### 闭包
#### JS中函数是一等公民
- 在JavaScript中，函数是非常重要的，并且是一等公民：
    - 那么就意味着函数的使用是非常灵活的
    - 函数可以作为另外一个函数的参数，也可以作为另外一个函数的返回值来使用
- 自己编写高阶函数
- 使用内置的高阶函数

#### JS中闭包的定义

1. 在计算机科学中对闭包的定义（维基百科）：
    - `闭包（英语：Closure）`，又称词法闭包（Lexical Closure）或函数闭包（function closures）
    - 是在支持 `头等函数` 的编程语言中，实现词法绑定的一种技术
    - 闭包在实现上是一个结构体，它存储了一个函数和一个关联的环境（相当于一个符号查找表）
    - 闭包跟函数最大的区别在于，当捕捉闭包的时候，它的 自由变量 会在补充时被确定，这样即使脱离了捕捉时的上下文，它也能照常运行
- 闭包的概念出现于60年代，最早实现闭包的程序是 Scheme，那么我们就可以理解为什么JavaScript中有闭包：
    - 因为JavaScript中有大量的设计是来源于Scheme的
2. MDN对JavaScript闭包的解释：
    - 一个函数和对其周围状态`（lexical environment，词法环境）`的引用捆绑在一起（或者说函数被引用包围），这样的组合就是`闭包（closure）`
    - 也就是说，闭包让你可以在一个内层函数中访问到其外层函数的作用域
    - 在 JavaScript 中，每当创建一个函数，闭包就会在函数创建的同时被创建出来
3. 总结：
    - 一个普通的函数function，如果它可以访问外层作用于的`自由变量`，那么这个函数就是一个闭包
    - 从广义的角度来说：JavaScript中的函数都是闭包
    - 从狭义的角度来说：**JavaScript中一个函数，如果访问了外层作用于的变量，那么它是一个闭包**

#### 闭包的访问过程

如果我们编写了如下的代码，它一定是形成了闭包的：

![闭包的访问过程](/image/02/%E9%97%AD%E5%8C%85%E7%9A%84%E8%AE%BF%E9%97%AE%E8%BF%87%E7%A8%8B.png)

#### 闭包的执行过程

当函数继续执行
- 这个时候makeAdder函数执行完毕，正常情况下我们的AO对象会被释放
- 但是因为在0xb00的函数中有作用域引用指向了这个AO对象，所以它不会被释放掉

![闭包的执行过程](/image/02/%E9%97%AD%E5%8C%85%E7%9A%84%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B.png)

#### 闭包的内存泄露

闭包是有内存泄露的
- 在上面的案例中，如果后续我们不再使用`add10`函数了，那么该函数对象应该要被销毁掉，并且其引用着的父
作用域`AO`也应该被销毁掉
- 但是目前因为在全局作用域下`add10`变量对`0xb00`的函数对象有引用，而`0xb00`的作用域中`AO（0x200）`有引
用，所以最终会造成这些内存都是无法被释放的
- 所以我们经常说的闭包会造成内存泄露，其实就是刚才的引用链中的所有对象都是无法释放的
- 解决
    - 当将add10设置为null时，就不再对函数对象0xb00有引用，那么对应的AO对象0x200也就不可达了
    - 在GC的下一次检测中，它们就会被销毁掉
    ```js
    add10 = null
    ```

#### AO不使用的属性

- js引擎会自动清除没有被引用的属性


## JS函数的this指向

### this指向

1. `this`在全局作用于下指向`window`

2. 函数中使用
    - 所有的函数在被调用时，都会创建一个执行上下文：
    - 这个上下文中记录着函数的`调用栈`、`AO对象`等
    - `this`也是其中的一条记录

3. 函数在调用时，JavaScript会默认给this绑定一个值
    - this的绑定和定义的位置（编写的位置）没有关系
    - this的绑定和调用方式以及调用的位置有关系
    - this是在运行时被绑定的

4. 绑定规则
    1. 默认绑定
    2. 隐式绑定
    3. 显示绑定
    4. `new`绑定

#### 规则一：默认绑定

> 独立的函数调用我们可以理解成函数没有被绑定到某个对象上进行调用

独立函数调用使用默认绑定

![this默认绑定](/image/03/this%E9%BB%98%E8%AE%A4%E7%BB%91%E5%AE%9A.png)

#### 规则二：隐式绑定

通过某个对象进行调用使用隐式绑定

![this隐式绑定](/image/03/this%E9%9A%90%E5%BC%8F%E7%BB%91%E5%AE%9A.png)

#### 规则三：显示绑定

隐式绑定有一个前提条件：
- 必须在调用的对象内部有一个对函数的引用（比如一个属性）
- 如果没有这样的引用，在进行调用时，会报找不到该函数的错误
- 正是通过这个引用，间接的将`this`绑定到了这个对象上

如果我们不希望在 对象内部 包含这个函数的引用，同时又希望在这个对象上进行强制调用，该怎么做呢？
- JavaScript所有的函数都可以使用`call`和`apply`方法（和Prototype有关）
    - 区别：第一个参数是相同的，后面的参数，`apply`为数组，`call`为参数列表
    - 这两个函数的第一个参数都要求是一个对象，这个对象就是给this准备的
    - 在调用这个函数时，会将this绑定到这个传入的对象上
- 因为上面的过程，我们明确的绑定了this指向的对象，所以称之为 **显示绑定**

##### call、apply、bind

- 通过`call`或者`apply`绑定`this`对象
    - 显示绑定后，`this`就会明确的指向绑定的对象
    ```js
    function foo() {
        console.log(this)
    }
    foo.call(window) //window
    foo.call({name: 'hidari'}) // {name: 'hidari'}
    foo.call(123) // Number(123)
    ```
- 如果我们希望一个函数总是显示的绑定到一个对象上，可以用`bind`
```js
function foo() {
    console.log(this)
}

var obj = {
    name: 'hidari'
}

var bar = foo.bind(obj)
bar() // obj对象
```

##### 内置函数的绑定思考

- 有些时候，我们会调用一些JavaScript的内置函数，或者一些第三方库中的内置函数。
    - 这些内置函数会要求我们传入另外一个函数；
    - 我们自己并不会显示的调用这些函数，而且JavaScript内部或者第三方库内部会帮助我们执行；
    - 这些函数中的`this`又是如何绑定的呢
- `setTimeout`、数组的`forEach`、`div`的点击
```js
setTimeout(function() {
    console.log(this) // window
}, 1000)
```
```js
var names = ['abc','cba']
var obj = { name: 'hidari' }
names.forEach(function (item) {
    console.log(this) // 三次 obj 对象
}, obj) // obj 为 this 绑定对象 thisArg 参数
```
```js
var box = document.querySelector('.box')
box.onclick = function () {
    console.log(this === box)
}
```

#### 规则四：显示绑定
- JavaScript中的函数可以当做一个类的构造函数来使用，也就是使用`new`关键字
- 使用`new`关键字来调用函数是，会执行如下的操作：
    1. 创建一个全新的对象
    2. 这个新对象会被执行`prototype`连接
    3. 这个新对象会绑定到函数调用的`this`上（`this`的绑定在这个步骤完成）
    4. 如果函数没有返回其他对象，表达式会返回这个新对象
```js
// 创建 Person
funtion Person(name) {
    console.log(this) // Person {}
    this.name = name // Person { name: 'hidari' }
}
var p = new Person('hidari')
console.log(p)
```

#### 规则优先级
1. 默认规则的优先级最低
> 毫无疑问，默认规则的优先级是最低的，因为存在其他规则时，就会通过其他规则的方式来绑定`this`
2. 显示绑定优先级高于隐式绑定
3. `new`绑定优先级高于隐式绑定
4. `new`绑定优先级高于`bind`
    - `new`绑定和`call`、`apply`是不允许同时使用的，所以不存在谁的优先级更高
    - `new`绑定可以和`bind`一起使用，`new`绑定优先级更高

#### this规则之外 – 忽略显示绑定

> 如果在显示绑定中，我们传入一个`null`或者`undefined`，那么这个显示绑定会被忽略，使用默认规则：

```js
funtion foo () {
    console.log(this)
}

var obj = { name: 'hidari'}

foo.call(null) // window
foo.call(undefined) // window

var bar = foo.bind(null)
bar() // window
```

#### this规则之外 - 间接函数引用

另外一种情况，创建一个函数的 间接引用，这种情况使用默认绑定规则
- 赋值`(obj2.foo = obj1.foo)`的结果是`foo`函数
- `foo`函数被直接调用，那么是默认绑定

```js
funtion foo () {
    console.log(this)
}

var obj1 = {
    name: 'obj1'
    foo: foo
}

var obj2 = { name: 'obj2'}

obj1.foo() // obj1
(obj2.foo = obj1.foo)() // window
```
#### this规则之外 – ES6箭头函数

> 箭头函数不使用this的四种标准规则（也就是不绑定this），而是根据外层作用域来决定this


#### 面试题
```js
var name = "window";

var person = {
  name: "person",
  sayName: function () {
    console.log(this.name);
  }
};

function sayName() {
  var sss = person.sayName;
  sss(); // window: 独立函数调用
  person.sayName(); // person: 隐式调用
  (person.sayName)(); // person: 隐式调用
  (b = person.sayName)(); // window: 赋值表达式(独立函数调用)
}

sayName();
```

```js
var name = 'window'

var person1 = {
  name: 'person1',
  foo1: function () {
    console.log(this.name)
  },
  foo2: () => console.log(this.name),
  foo3: function () {
    return function () {
      console.log(this.name)
    }
  },
  foo4: function () {
    return () => {
      console.log(this.name)
    }
  }
}

var person2 = { name: 'person2' }

person1.foo1(); // person1(隐式绑定)
person1.foo1.call(person2); // person2(显示绑定优先级大于隐式绑定)

person1.foo2(); // window(不绑定作用域,上层作用域是全局)
person1.foo2.call(person2); // window

person1.foo3()(); // window(独立函数调用)
person1.foo3.call(person2)(); // window(独立函数调用)
person1.foo3().call(person2); // person2(最终调用返回函数式, 使用的是显示绑定)

person1.foo4()(); // person1(箭头函数不绑定this, 上层作用域this是person1)
person1.foo4.call(person2)(); // person2(上层作用域被显示的绑定了一个person2)
person1.foo4().call(person2); // person1(上层找到person1)
```

```js
var name = 'window'

function Person (name) {
  this.name = name
  this.foo1 = function () {
    console.log(this.name)
  },
  this.foo2 = () => console.log(this.name),
  this.foo3 = function () {
    return function () {
      console.log(this.name)
    }
  },
  this.foo4 = function () {
    return () => {
      console.log(this.name)
    }
  }
}

var person1 = new Person('person1')
var person2 = new Person('person2')

person1.foo1() // person1
person1.foo1.call(person2) // person2(显示高于隐式绑定)

person1.foo2() // person1 (上层作用域中的this是person1)
person1.foo2.call(person2) // person1 (上层作用域中的this是person1)

person1.foo3()() // window(独立函数调用)
person1.foo3.call(person2)() // window
person1.foo3().call(person2) // person2

person1.foo4()() // person1
person1.foo4.call(person2)() // person2
person1.foo4().call(person2) // person1


var obj = {
  name: "obj",
  foo: function() {

  }
}
```

```js
var name = 'window'

function Person (name) {
  this.name = name
  this.obj = {
    name: 'obj',
    foo1: function () {
      return function () {
        console.log(this.name)
      }
    },
    foo2: function () {
      return () => {
        console.log(this.name)
      }
    }
  }
}

var person1 = new Person('person1')
var person2 = new Person('person2')

person1.obj.foo1()() // window
person1.obj.foo1.call(person2)() // window
person1.obj.foo1().call(person2) // person2

person1.obj.foo2()() // obj
person1.obj.foo2.call(person2)() // person2
person1.obj.foo2().call(person2) // obj



// 上层作用域的理解
var obj = {
  name: "obj",
  foo: function() {
    // 上层作用域是全局
  }
}

function Student() {
  this.foo = function() {}
}
```

## JS函数式编程

### 实现apply、call、bind

### call
```js
// apply/call/bind的用法

// 给所有的函数添加一个hycall的方法
Function.prototype.hycall = function(thisArg, ...args) {
  // 在这里可以去执行调用的那个函数(foo)
  // 问题: 得可以获取到是哪一个函数执行了hycall
  // 1.获取需要被执行的函数
  var fn = this

  // 2.对thisArg转成对象类型(防止它传入的是非对象类型)
  thisArg = (thisArg !== null && thisArg !== undefined) ? Object(thisArg): window

  // 3.调用需要被执行的函数
  thisArg.fn = fn
  var result = thisArg.fn(...args)
  delete thisArg.fn

  // 4.将最终的结果返回出去
  return result
}


function foo() {
  console.log("foo函数被执行", this)
}

function sum(num1, num2) {
  console.log("sum函数被执行", this, num1, num2)
  return num1 + num2
}


// 系统的函数的call方法
foo.call(undefined)
var result = sum.call({}, 20, 30)
// console.log("系统调用的结果:", result)

// 自己实现的函数的hycall方法
// 默认进行隐式绑定
// foo.hycall({name: "why"})
foo.hycall(undefined)
var result = sum.hycall("abc", 20, 30)
console.log("hycall的调用:", result)

// var num = {name: "why"}
// console.log(Object(num))
```

#### apply
```js
// 自己实现hyapply
Function.prototype.hyapply = function(thisArg, argArray) {
  // 1.获取到要执行的函数
  var fn = this

  // 2.处理绑定的thisArg
  thisArg = (thisArg !== null && thisArg !== undefined) ? Object(thisArg): window

  // 3.执行函数
  thisArg.fn = fn
  var result
  // if (!argArray) { // argArray是没有值(没有传参数)
  //   result = thisArg.fn()
  // } else { // 有传参数
  //   result = thisArg.fn(...argArray)
  // }

  // argArray = argArray ? argArray: []
  argArray = argArray || []
  result = thisArg.fn(...argArray)

  delete thisArg.fn

  // 4.返回结果
  return result
}

function sum(num1, num2) {
  console.log("sum被调用", this, num1, num2)
  return num1 + num2
}

function foo(num) {
  return num
}

function bar() {
  console.log("bar函数被执行", this)
}

// 系统调用
// var result = sum.apply("abc", 20)
// console.log(result)

// 自己实现的调用
// var result = sum.hyapply("abc", [20, 30])
// console.log(result)

// var result2 = foo.hyapply("abc", [20])
// console.log(result2)

// edge case
bar.hyapply(0)
```

#### bind
```js
Function.prototype.hybind = function(thisArg, ...argArray) {
  // 1.获取到真实需要调用的函数
  var fn = this

  // 2.绑定this
  thisArg = (thisArg !== null && thisArg !== undefined) ? Object(thisArg): window

  function proxyFn(...args) {
    // 3.将函数放到thisArg中进行调用
    thisArg.fn = fn
    // 特殊: 对两个传入的参数进行合并
    var finalArgs = [...argArray, ...args]
    var result = thisArg.fn(...finalArgs)
    delete thisArg.fn

    // 4.返回结果
    return result
  }

  return proxyFn
}

function foo() {
  console.log("foo被执行", this)
  return 20
}

function sum(num1, num2, num3, num4) {
  console.log(num1, num2, num3, num4)
}

// 系统的bind使用
var bar = foo.bind("abc")
bar()

// var newSum = sum.bind("aaa", 10, 20, 30, 40)
// newSum()

// var newSum = sum.bind("aaa")
// newSum(10, 20, 30, 40)

// var newSum = sum.bind("aaa", 10)
// newSum(20, 30, 40)


// 使用自己定义的bind
// var bar = foo.hybind("abc")
// var result = bar()
// console.log(result)

var newSum = sum.hybind("abc", 10, 20)
var result = newSum(30, 40)
```

#### arguments

- `arguments` 是一个 对应于 传递给函数的参数 的 `类数组(array-like)`对象。
- `array-like`意味着它不是一个数组类型，而是一个对象类型：
    - 但是它却拥有数组的一些特性，比如说`length`，比如可以通过`index`索引来访问；
    - 但是它却没有数组的一些方法，比如`forEach`、`map`等
- `arguments`转成`array`

```js
function foo(num1, num2) {
  // 1.自己遍历
  var newArr = []
  for (var i = 0; i < arguments.length; i++) {
    newArr.push(arguments[i])
  }
  console.log(newArr)

  // 2.arguments转成array类型
  // 2.1.自己遍历arguments中所有的元素

  // 2.2.Array.prototype.slice将arguments转成array
  var newArr2 = Array.prototype.slice.call(arguments)
  console.log(newArr2)

  var newArr3 = [].slice.call(arguments)
  console.log(newArr3)

  // 2.3.ES6的语法
  var newArr4 = Array.from(arguments)
  console.log(newArr4)
  var newArr5 = [...arguments]
  console.log(newArr5)
}

foo(10, 20, 30, 40, 50)

// 额外补充的知识点: Array中的slice实现
Array.prototype.hyslice = function(start, end) {
  var arr = this
  start = start || 0
  end = end || arr.length
  var newArray = []
  for (var i = start; i < end; i++) {
    newArray.push(arr[i])
  }
  return newArray
}

var newArray = Array.prototype.hyslice.call(["aaaa", "bbb", "cccc"], 1, 3)
console.log(newArray)

var names = ["aaa", "bbb", "ccc", "ddd"]
names.slice(1, 3)
```

#### 箭头函数不绑定arguments

> 箭头函数是不绑定`arguments`的，所以我们在箭头函数中使用`arguments`会去上层作用域查找

```js
// 1.案例一:
var foo = () => {
  console.log(arguments)
}

// foo()

// 2.案例二:
function foo() {
  var bar = () => {
    console.log(arguments)
  }
  return bar
}

var fn = foo(123)
fn()

// 3.案例三:
var foo = (num1, num2, ...args) => {
  console.log(args)
}

foo(10, 20, 30, 40, 50)

```

### JavaScript纯函数

- 函数式编程中有一个非常重要的概念叫纯函数，JavaScript符合函数式编程的范式，所以也有纯函数的概念
    - 在`react`开发中纯函数是被多次提及的
    - 比如`react`中组件就被要求像是一个纯函数（为什么是像，因为还有`class`组件），`redux`中有一个`reducer`的概念，也是要求必须是一个纯函数
- 纯函数的维基百科定义：
    - 在程序设计中，若一个函数符合以下条件，那么这个函数被称为纯函数：
    - 此函数在相同的输入值时，需产生相同的输出
    - 函数的输出和输入值以外的其他隐藏信息或状态无关，也和由I/O设备产生的外部输出无关
    - 该函数不能有语义上可观察的函数副作用，诸如“触发事件”，使输出设备输出，或更改输出值以外物件的内容等
- 总结：
    - 确定的输入，一定会产生确定的输出
    - 函数在执行过程中，不能产生副作用
        - 副作用表示在执行一个函数时，除了返回函数值之外，还对调用函数产生了附加的影响，比如`修改了全局变量`，`修改参数`或者`改变外部的存储`

#### 纯函数的案例

对数组操作的两个函数：
- `slice`：`slice`截取数组时不会对原数组进行任何操作,而是生成一个新的数组
- `splice`：`splice`截取数组, 会返回一个新的数组, 也会对原数组进行修改
- `slice`就是一个纯函数，不会修改传入的参数

```js
var names = ["abc", "cba", "nba", "dna"]

// slice只要给它传入一个start/end, 那么对于同一个数组来说, 它会给我们返回确定的值
// slice函数本身它是不会修改原来的数组
// slice -> this
// slice函数本身就是一个纯函数
var newNames1 = names.slice(0, 3)
console.log(newNames1)
console.log(names)

// ["abc", "cba", "nba", "dna"]
// splice在执行时, 有修改掉调用的数组对象本身, 修改的这个操作就是产生的副作用
// splice不是一个纯函数
var newNames2 = names.splice(2)
console.log(newNames2)
console.log(names)
```

#### 纯函数的优势

- 写的时候保证了函数的纯度，只是单纯实现自己的业务逻辑即可，不需要关心传入的内容是如何获得的或者依赖其他的外部变量是否已经发生了修改
- 在用的时候，确定输入内容不会被任意篡改，并且自己确定的输入，一定会有确定的输出
- `React`中就要求我们无论是函数还是`class`声明一个组件，这个组件都必须像纯函数一样，保护它们的`props`不被修改

### JavaScript柯里化

维基百科的解释：
- 在计算机科学中，柯里化（英语：Currying），又译为卡瑞化或加里化
- 是把接收多个参数的函数，变成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数，而且返回结果的新函数的技术
- 柯里化声称 “如果你固定某些参数，你将得到接受余下参数的一个函数”

总结：
- 只传递给函数一部分参数来调用它，让它返回一个函数去处理剩余的参数
- 这个过程就称之为柯里化


#### 柯里化的结构

```js
function add(x, y, z) {
  return x + y + z
}

var result = add(10, 20, 30)
console.log(result)

function sum1(x) {
  return function(y) {
    return function(z) {
      return x + y + z
    }
  }
}

var result1 = sum1(10)(20)(30)
console.log(result1)

// 简化柯里化的代码
var sum2 = x => y => z => {
  return x + y + z
}

console.log(sum2(10)(20)(30))

var sum3 = x => y => z => x + y + z
console.log(sum3(10)(20)(30))
```

#### 柯里化作用

1. 让函数的职责单一
- 在函数式编程中，我们其实往往希望一个函数处理的问题尽可能的单一，而不是将一大堆的处理过程交给一个函数来处理
- 那么我们是否就可以将每次传入的参数在单一的函数中进行处理，处理完后在下一个函数中再使用处理后的结果
2. 复用参数逻辑：
- `makeAdder`函数要求我们传入一个`num`（并且如果我们需要的话，可以在这里对`num`进行一些修改）；
- 在之后使用返回的函数时，我们不需要再继续传入`num`了
```js
// function sum(m, n) {
//   return m + n
// }

// // 假如在程序中,我们经常需要把5和另外一个数字进行相加
// console.log(sum(5, 10))
// console.log(sum(5, 14))
// console.log(sum(5, 1100))
// console.log(sum(5, 555))

function makeAdder(count) {
count = count * count

return function(num) {
    return count + num
}
}

// var result = makeAdder(5)(10)
// console.log(result)
var adder5 = makeAdder(5)
adder5(10)
adder5(14)
adder5(1100)
adder5(555)
```
- 打印日志中的柯里化
```js
function log(date, type, message) {
  console.log(`[${date.getHours()}:${date.getMinutes()}][${type}]: [${message}]`)
}

// log(new Date(), "DEBUG", "查找到轮播图的bug")
// log(new Date(), "DEBUG", "查询菜单的bug")
// log(new Date(), "DEBUG", "查询数据的bug")

// 柯里化的优化
var log = date => type => message => {
  console.log(`[${date.getHours()}:${date.getMinutes()}][${type}]: [${message}]`)
}

// 如果我现在打印的都是当前时间
var nowLog = log(new Date())
nowLog("DEBUG")("查找到轮播图的bug")
nowLog("FETURE")("新增了添加用户的功能")

var nowAndDebugLog = log(new Date())("DEBUG")
nowAndDebugLog("查找到轮播图的bug")
nowAndDebugLog("查找到轮播图的bug")
nowAndDebugLog("查找到轮播图的bug")
nowAndDebugLog("查找到轮播图的bug")


var nowAndFetureLog = log(new Date())("FETURE")
nowAndFetureLog("添加新功能~")
```

#### 自动柯里化函数
```js
// 柯里化函数的实现hyCurrying
function hyCurrying(fn) {
  function curried(...args) {
    // 判断当前已经接收的参数的个数, 可以参数本身需要接受的参数是否已经一致了
    // 1.当已经传入的参数 大于等于 需要的参数时, 就执行函数
    if (args.length >= fn.length) {
      // fn(...args)
      // fn.call(this, ...args)
      return fn.apply(this, args)
    } else {
      // 没有达到个数时, 需要返回一个新的函数, 继续来接收的参数
      function curried2(...args2) {
        // 接收到参数后, 需要递归调用curried来检查函数的个数是否达到
        return curried.apply(this, args.concat(args2))
      }
      return curried2
    }
  }
  return curried
}
```

### 组合函数

- 组合（Compose）函数是在JavaScript开发过程中一种对函数的使用技巧、模式：
    - 比如我们现在需要对某一个数据进行函数的调用，执行两个函数fn1和fn2，这两个函数是依次执行的
    - 那么如果每次我们都需要进行两个函数的调用，操作上就会显得重复
    - 可以将这两个函数组合起来，自动依次调用
    - 这个过程就是对函数的组合，我们称之为 **组合函数（Compose Function）**

```js
function hyCompose(...fns) {
  var length = fns.length
  // 遍历所有的参数 如果不是函数 报错
  for (var i = 0; i < length; i++) {
    if (typeof fns[i] !== 'function') {
      throw new TypeError("Expected arguments are functions")
    }
  }

  // 取出所有函数 依次调用
  function compose(...args) {
    var index = 0
    var result = length ? fns[index].apply(this, args): args
    while(++index < length) {
      result = fns[index].call(this, result)
    }
    return result
  }
  return compose
}

function double(m) {
  return m * 2
}

function square(n) {
  return n ** 2
}

var newFn = hyCompose(double, square)
console.log(newFn(10))
```

## JS额外知识补充

### with语句

> with语句 扩展一个语句的作用域链

```js
"use strict";

var message = "Hello World"
// console.log(message)

// with语句: 可以形成自己的作用域
var obj = {name: "why", age: 18, message: "obj message"}

function foo() {
  function bar() {
    with(obj) {
      console.log(message)
      console.log("------")
    }
  }
  bar()
}

foo()

var info = {name: "kobe"}
with(info) {
  console.log(name)
}
```

- 不建议使用with语句，因为它可能是混淆错误和兼容性问题的根源

### eval函数

- eval是一个特殊的函数，它可以将传入的字符串当做JavaScript代码来运行

```js
var jsString = 'var message = "Hello World"; console.log(message);'

var message = "Hello World"
console.log(message)

eval(jsString)
```

- 不建议在开发中使用`eval`：
    - `eval`代码的可读性非常的差（代码的可读性是高质量代码的重要原则）
    - `eval`是一个字符串，那么有可能在执行的过程中被刻意篡改，那么可能会造成被攻击的风险
    - `eval`的执行必须经过JS解释器，不能被JS引擎优化

### 严格模式

- 在`ECMAScript5`标准中，JavaScript提出了`严格模式`的概念（Strict Mode）：
    - 严格模式很好理解，是一种具有限制性的JavaScript模式，从而使代码隐式的脱离了 `懒散（sloppy）模式`
    - 支持严格模式的浏览器在检测到代码中有严格模式时，会以更加严格的方式对代码进行检测和执行
- 严格模式对正常的JavaScript语义进行了一些限制：
    - 严格模式通过 抛出错误 来消除一些原有的 `静默（silent）错误`
    - 严格模式让JS引擎在执行代码时可以进行更多的优化（不需要对一些特殊的语法进行处理）
    - 严格模式禁用了在`ECMAScript`未来版本中可能会定义的一些语法
- 严格模式支持粒度话的迁移：
    - 可以支持在js文件中开启严格模式
    - 也支持对某一个函数开启严格模式
- 严格模式通过在文件或者函数开头使用 `use strict` 来开启。
- 严格模式限制：
    1. 无法意外的创建全局变量
    2. 严格模式会使引起`静默失败(silently fail,注:不报错也没有任何效果)`的赋值操作抛出异常
    3. 严格模式下试图删除不可删除的属性
    4. 严格模式不允许函数参数有相同的名称
    5. 不允许`0`的八进制语法
    6. 在严格模式下，不允许使用`with`
    7. 在严格模式下，`eval`不再为上层引用变量
    8. 严格模式下，`this`绑定不会默认转成对象

## JS面向对象

JavaScript支持多种编程范式的，包括函数式编程和面向对象编程：
- JavaScript中的对象被设计成一组属性的无序集合，像是一个哈希表，有`key`和`value`组成；
- `key`是一个标识符名称，`value`可以是任意类型，也可以是其他对象或者函数类型；
- 如果值是一个函数，那么我们可以称之为是对象的方法

- 创建对象的两种方式
```js
// 创建一个对象, 对某一个人进行抽象(描述)
// 1.创建方式一: 通过new Object()创建
var obj = new Object()
obj.name = "why"
obj.age = 18
obj.height = 1.88
obj.running = function() {
  console.log(this.name + "在跑步~")
}

// 2.创建方式二: 字面量形式
var info = {
  name: "kobe",
  age: 40,
  height: 1.98,
  eating: function() {
    console.log(this.name + "在吃东西~")
  }
}
```

### 对属性操作的控制

- 如果我们想要对一个属性进行比较精准的操作控制，那么我们就可以使用属性描述符
    - 通过属性描述符可以精准的添加或修改对象的属性
    - 属性描述符需要使用 `Object.defineProperty` 来对属性进行添加或者修改
- Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象
    - 可接收三个参数：
        - `obj`要定义属性的对象；
        - `prop`要定义或修改的属性的名称或 `Symbol`
        - `descriptor`要定义或修改的属性描述符
    - 返回值：被传递给函数的对象
- 属性描述符的类型有两种：
    - 数据属性（Data Properties）描述符（Descriptor）
    - 存取属性（Accessor访问器 Properties）描述符（Descriptor）

![属性描述符两种类型](/image/04/%E5%B1%9E%E6%80%A7%E6%8F%8F%E8%BF%B0%E7%AC%A6%E4%B8%A4%E7%A7%8D%E5%88%86%E7%B1%BB.PNG)

#### 数据属性描述符

数据数据描述符有如下四个特性：
- `[[Configurable]]`：表示属性是否可以通过`delete`删除属性，是否可以修改它的特性，或者是否可以将它修改为存取属性描述符；
    - 当我们直接在一个对象上定义某个属性时，这个属性的`[[Configurable]]`为`true`
    - 当我们通过属性描述符定义一个属性时，这个属性的`[[Configurable]]`默认为`false`
- `[[Enumerable]]`：表示属性是否可以通过`for-in`或者`Object.keys()`返回该属性
    - 当我们直接在一个对象上定义某个属性时，这个属性的`[[Enumerable]]`为`true`
    - 当我们通过属性描述符定义一个属性时，这个属性的`[[Enumerable]]`默认为`false`
- `[[Writable]]`：表示是否可以修改属性的值
    - 当我们直接在一个对象上定义某个属性时，这个属性的`[[Writable]]`为`true`
    - 当我们通过属性描述符定义一个属性时，这个属性的`[[Writable]]`默认为`false`
- `[[value]]`：属性的`value`值，读取属性时会返回该值，修改属性时，会对其进行修改
    - 默认情况下这个值是`undefined`

#### 存取属性描述符

数据数据描述符有如下四个特性：
- `[[Configurable]]`：表示属性是否可以通过`delete`删除属性，是否可以修改它的特性，或者是否可以将它修改为存取属性
描述符
    - 和数据属性描述符是一致的
    - 当我们直接在一个对象上定义某个属性时，这个属性的[[Configurable]]为true
    - 当我们通过属性描述符定义一个属性时，这个属性的[[Configurable]]默认为false
- `[[Enumerable]]`：表示属性是否可以通过`for-in`或者`Object.keys()`返回该属性
    - 和数据属性描述符是一致的
    - 当我们直接在一个对象上定义某个属性时，这个属性的`[[Enumerable]]`为`true`
    - 当我们通过属性描述符定义一个属性时，这个属性的`[[Enumerable]]`默认为`false`
- `[[get]]`：获取属性时会执行的函数。默认为`undefined`
- `[[set]]`：设置属性时会执行的函数。默认为`undefined`

#### 同时定义多个属性

> `Object.defineProperties()`方法直接在一个对象上定义 多个 新的属性或修改现有属性，并且返回该对象。

```js
var obj = {
  // 私有属性(js里面是没有严格意义的私有属性)
  _age: 18,
  _eating: function() {},
  set age(value) {
    this._age = value
  },
  get age() {
    return this._age
  }
}

Object.defineProperties(obj, {
  name: {
    configurable: true,
    enumerable: true,
    writable: true,
    value: "why"
  },
  age: {
    configurable: true,
    enumerable: true,
    get: function() {
      return this._age
    },
    set: function(value) {
      this._age = value
    }
  }
})

obj.age = 19
console.log(obj.age)

console.log(obj)
```

#### 对象方法补充

- 获取对象的属性描述符：
    - `getOwnPropertyDescriptor`
    - `getOwnPropertyDescriptors`
- 禁止对象扩展新属性：`preventExtensions`
    - 给一个对象添加新的属性会失败（在严格模式下会报错）
- 密封对象，不允许配置和删除属性：`seal`
    - 实际是调用`preventExtensions`
    - 并且将现有属性的`configurable:false`
- 冻结对象，不允许修改现有属性： `freeze`
    - 实际上是调用`seal`
    - 并且将现有属性的`writable: false`

### 创建多个对象的方案

- 如果我们现在希望创建一系列的对象：比如`Person`对象
    - 包括张三、李四、王五、李雷等等，他们的信息各不相同
    - 那么采用什么方式来创建比较好呢

#### 工厂模式

- 工厂模式其实是一种常见的设计模式
- 通常我们会有一个工厂方法，通过该工厂方法我们可以产生想要的对象

```js
// 工厂模式: 工厂函数
function createPerson(name, age, height, address) {
  var p = {}
  p.name = name
  p.age = age
  p.height = height;
  p.address = address

  p.eating = function() {
    console.log(this.name + "在吃东西~")
  }

  p.running = function() {
    console.log(this.name + "在跑步~")
  }

  return p
}

var p1 = createPerson("张三", 18, 1.88, "广州市")
var p2 = createPerson("李四", 20, 1.98, "上海市")
var p3 = createPerson("王五", 30, 1.78, "北京市")

// 工厂模式的缺点(获取不到对象最真实的类型)
console.log(p1, p2, p3)
```

#### 构造函数
- 工厂方法创建对象有一个比较大的问题：我们在打印对象时，对象的类型都是`Object`类型
    - 但是从某些角度来说，这些对象应该有一个他们共同的类型
- 什么是构造函数
    - 构造函数也称之为`构造器（constructor）`，通常是我们在创建对象时会调用的函数
    - 在其他面向的编程语言里面，构造函数是存在于类中的一个方法，称之为构造方法
    - 但是JavaScript中的构造函数有点不太一样
- JavaScript中的构造函数是怎么样的？
    - 构造函数也是一个普通的函数，从表现形式来说，和普通的函数没有任何区别
    - 那么如果这么一个普通的函数被使用`new`操作符来调用了，那么这个函数就称之为是一个构造函数
- new操作符调用的作用
    - 如果一个函数被使用new操作符调用了，那么它会执行如下操作：
    1. 在内存中创建一个新的对象（空对象）
    2. 这个对象内部的`[[prototype]]`属性会被赋值为该构造函数的`prototype`属性
    3. 构造函数内部的`this`，会指向创建出来的新对象
    4. 执行函数的内部代码（函数体代码）
    5. 如果构造函数没有返回非空对象，则返回创建出来的新对象
- 构造函数也是有缺点的，它在于我们需要为每个对象的函数去创建一个函数对象实例

#### 对象的原型

JavaScript当中每个对象都有一个特殊的内置属性 `[[prototype]]`，这个特殊的对象可以指向另外一个对象。
- 那么这个对象有什么用呢？
    - 当我们通过引用对象的属性`key`来获取一个`value`时，它会触发 `[[Get]]`的操作
    - 这个操作会首先检查该属性是否有对应的属性，如果有的话就使用它
    - 如果对象中没有改属性，那么会访问对象`[[prototype]]`内置属性指向的对象上的属性
- 那么如果通过字面量直接创建一个对象，这个对象也会有这样的属性吗？如果有，应该如何获取这个属性呢？
    - 答案是有的，只要是对象都会有这样的一个内置属性
- 获取的方式有两种：
    - 方式一：通过对象的 `__proto__` 属性可以获取到（但是这个是早期浏览器自己添加的，存在一定的兼容性问题）
    - 方式二：通过 `Object.getPrototypeOf` 方法可以获取到

#### 函数的原型 prototype

> 所有的函数都有一个`prototype`的属性

- 因为函数是一个函数，才有`prototype`属性

- `new`操作符
> `new`关键字的步骤：
1. 在内存中创建一个新的对象（空对象）
2. 这个对象内部的`[[prototype]]`属性会被赋值为该构造函数的`prototype`属性
- 那么也就意味着我们通过`Person`构造函数创建出来的所有对象的`[[prototype]]`属性都指向`Person.prototype`

![创建对象的内存表现](/image/04/%E5%88%9B%E5%BB%BA%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E5%AD%98%E8%A1%A8%E7%8E%B0.png)

![赋值为新的对象](/image/04/%E8%B5%8B%E5%80%BC%E4%B8%BA%E6%96%B0%E7%9A%84%E5%AF%B9%E8%B1%A1.png)

![prototype添加属性](/image/04/prototype%E6%B7%BB%E5%8A%A0%E5%B1%9E%E6%80%A7.png)

- `constructor`属性
    - 事实上原型对象上面是有一个属性的：`constructor`
    - 默认情况下原型上都会添加一个属性叫做`constructor`，这个`constructor`指向当前的函数对象

#### 重写原型对象

- 如果我们需要在原型上添加过多的属性，通常我们会重新整个原型对象：
```js
function Person() {}

Person.prototype = {
    name: 'hidari'
}
```
- 前面我们说过, 每创建一个函数, 就会同时创建它的`prototype`对象, 这个对象也会自动获取`constructor`属性；
    - 而我们这里相当于给`prototype`重新赋值了一个对象, 那么这个新对象的`constructor`属性, 会指向`Object`构造函数, 而不是`Person`构造函数了

- 如果希望`constructor`指向`Person`，那么可以手动添加：
- 上面的方式虽然可以, 但是也会造成`constructor`的`[[Enumerable]]`特性被设置了`true`.
    - 默认情况下, 原生的`constructor`属性是不可枚举的.
    - 如果希望解决这个问题, 就可以使用我们前面介绍的`Object.defineProperty()`函数了

```js
Person.prototype = {
    constructor: Person,
    name: 'hidari'
}
Object.defineProperty(Person.prototype, "constructor", {
    enumerable: false,
    value: Person
})
```

### 面向对象的特性 – 继承

面向对象有三大特性：封装、继承、多态
- 封装：我们前面将属性和方法封装到一个类中，可以称之为封装的过程；
- 继承：继承是面向对象中非常重要的，不仅仅可以减少重复代码的数量，也是多态前提（纯面向对象中）；
- 多态：不同的对象在执行时表现出不同的形态；

#### JavaScript原型链

- 从一个对象上获取属性，如果在当前对象中没有获取到就会去它的原型上面获取

![原型链](/image/05/%E5%8E%9F%E5%9E%8B%E9%93%BE.png)

- Object的原型
- `[Object: null prototype] {}` 原型特殊的地方：
    - 特殊一：该对象有原型属性，但是它的原型属性已经指向的是`null`，也就是已经是顶层原型了
    - 特殊二：该对象上有很多默认的属性和方法
- 创建Object对象的内存图
![创建Object对象的内存图](/image/05/%E5%88%9B%E5%BB%BAObject%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)
- 原型链关系的内存图
![原型链关系的内存图](/image/05/%E5%8E%9F%E5%9E%8B%E9%93%BE%E5%85%B3%E7%B3%BB%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)
- Object是所有类的父类
![Object是所有类的父类](/image/05/Object%E6%98%AF%E6%89%80%E6%9C%89%E7%B1%BB%E7%9A%84%E7%88%B6%E7%B1%BB.png)

#### 通过原型链实现继承

- 如果我们现在需要实现继承，那么就可以利用原型链来实现了：
    - 目前stu的原型是p对象，而p对象的原型是Person默认的原型，里面包含running等函数；
    - 注意：步骤4和步骤5不可以调整顺序，否则会有问题
```js
// 1. 定义父类构造函数: 公共属性和方法
function Person() {
  this.name = "why"
  this.friends = []
}

// 2. 父类原型上添加内容
Person.prototype.eating = function() {
  console.log(this.name + " eating~")
}

// 3. 定义子类构造函数: 特有属性和方法
function Student() {
  this.sno = 111
}

// 4. 创建父类对象 作为子类的原型对象
var p = new Person()
Student.prototype = p

// 5. 在子类原型上添加内容
Student.prototype.studying = function() {
  console.log(this.name + " studying~")
}


// name/sno
var stu = new Student()

// console.log(stu.name)
// stu.eating()

// stu.studying()


// 原型链实现继承的弊端:
// 1.第一个弊端: 打印stu对象, 继承的属性是看不到的
console.log(stu.name)

// 2.第二个弊端: 创建出来两个stu的对象
var stu1 = new Student()
var stu2 = new Student()

// 直接修改对象上的属性, 是给本对象添加了一个新属性
stu1.name = "kobe"
console.log(stu2.name)

// 获取引用, 修改引用中的值, 会相互影响
stu1.friends.push("kobe")

console.log(stu1.friends)
console.log(stu2.friends)

// 3.第三个弊端: 在前面实现类的过程中都没有传递参数
var stu3 = new Student("lilei", 112)
```
- 继承创建子类的内存图
![继承创建子类的内存图](/image/05/%E7%BB%A7%E6%89%BF%E5%88%9B%E5%BB%BA%E5%AD%90%E7%B1%BB%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)

- 原型链继承的弊端：某些属性其实是保存在p对象上的；
1. 我们通过直接打印对象是看不到这个属性的；
2. 这个属性会被多个对象共享，如果这个对象是一个引用类型，那么就会造成问题；
3. 不能给Person传递参数，因为这个对象是一次性创建的（没办法定制化）

#### 借用构造函数继承

- 借用继承的做法非常简单：在子类型构造函数的内部调用父类型构造函数.
    - 因为函数可以在任意的时刻被调用；
    - 因此通过apply()和call()方法也可以在新创建的对象上执行构造函数

![借用构造函数继承内存图](/image/05/%E5%80%9F%E7%94%A8%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0%E7%BB%A7%E6%89%BF%E5%86%85%E5%AD%98%E5%9B%BE.png)

- 组合借用继承的问题
    - 组合继承最大的问题就是无论在什么情况下，都会调用两次父类构造函数。
        - 一次在创建子类原型的时候
        - 另一次在子类构造函数内部(也就是每次创建子类实例的时候)
    - 所有的子类实例事实上会拥有两份父类的属性
        - 一份在当前的实例自己里面(也就是person本身的)，另一份在子类对应的原型对象中(也就是person.__proto__里面)

#### 原型式继承函数

> JavaScript想实现继承的目的：重复利用另外一个对象的属性和方法

```js
var obj = {
  name: "why",
  age: 18
}

var info = Object.create(obj)

// 原型式继承函数
function createObject1(o) {
  var newObj = {}
  Object.setPrototypeOf(newObj, o)
  return newObj
}

function createObject2(o) {
  function Fn() {}
  Fn.prototype = o
  var newObj = new Fn()
  return newObj
}

// var info = createObject2(obj)
var info = Object.create(obj)
console.log(info)
console.log(info.__proto__)
```

#### 寄生式继承函数

> 寄生式继承的思路是结合原型类继承和工厂模式的一种方式
> 即创建一个封装继承过程的函数, 该函数在内部以某种方式来增强对象，最后再将这个对象返回

```js
var personObj = {
  running: function() {
    console.log("running")
  }
}

function createStudent(name) {
  var stu = Object.create(personObj)
  stu.name = name
  stu.studying = function() {
    console.log("studying~")
  }
  return stu
}

var stuObj = createStudent("why")
var stuObj1 = createStudent("kobe")
var stuObj2 = createStudent("james")
```

#### 寄生组合式继承

理想的组合继承
- 组合继承是比较理想的继承方式, 但是存在两个问题:
    - 问题一: 构造函数会被调用两次: 一次在创建子类型原型对象的时候, 一次在创建子类型实例的时候.
    - 问题二: 父类型中的属性会有两份: 一份在原型对象中, 一份在子类型实例中

寄生式继承将这两个问题给解决掉
- 当我们在子类型的构造函数中调用父类型`.call(this, 参数)`这个函数的时候, 就会将父类型中
的属性和方法复制一份到了子类型中. 所以父类型本身里面的内容, 我们不再需要
- 这个时候, 我们还需要获取到一份父类型的原型对象中的属性和方法.
- 能不能直接让子类型的原型对象 = 父类型的原型对象呢?
- 不要这么做, 因为这么做意味着以后修改了子类型原型对象的某个引用类型的时候, 父类型原生对象的引用类型也会被修改.
- 我们使用前面的寄生式思想就可以了

```js
// 定义 createObject 函数 返回 object 的实例
function createObject(o) {
  function Fn() {}
  Fn.prototype = o
  return new Fn()
}


/**
 * 继承式核心函数
 * @param SubType 子函数
 * @param SuperType 父函数
 */
function inheritPrototype(SubType, SuperType) {
  SubType.prototype = Object.create(SuperType.prototype)
//   SubType.prototype = createObject(SuperType.prototype)
  Object.defineProperty(SubType.prototype, "constructor", {
    enumerable: false,
    configurable: true,
    writable: true,
    value: SubType
  })
}

function Person(name, age, friends) {
  this.name = name
  this.age = age
  this.friends = friends
}

inheritPrototype(Student, Person)
```

#### 对象的方法补充

1. `hasOwnProperty`：对象是否有某一个属于自己的属性（不是在原型上的属性）
2. `in`/`for in` 操作符：判断某个属性是否在某个对象或者对象的原型上
3. `instanceof`：用于检测构造函数的`prototype`，是否出现在某个实例对象的原型链上
4. `isPrototypeOf`：用于检测某个对象，是否出现在某个实例对象的原型链上


#### 原型继承关系

> `function Function(){}` 的 `prototype` 和 `__proto__` 都是 `Function`
> __proto__ => 因为函数也是对象 指向对象
> `prototype` => 因为是一个函数 所以有 `prototype` 属性 指向 `Funtion`

![原型继承关系](/image/05/%E5%8E%9F%E5%9E%8B%E7%BB%A7%E6%89%BF%E5%85%B3%E7%B3%BB.png)

### 类

- 类的构造函数
- 当我们通过`new`关键字操作类的时候，会调用这个`constructor`函数，并且执行如下操作：
1. 在内存中创建一个新的对象（空对象）
2. 这个对象内部的`[[prototype]]`属性会被赋值为该类的`prototype`属性
3. 构造函数内部的`this`，会指向创建出来的新对象
4. 执行构造函数的内部代码（函数体代码）
5. 如果构造函数没有返回非空对象，则返回创建出来的新对象

- 类的实例方法
    - 对于实例的方法，我们是希望放到原型上的，这样可以被多个实例来共享
    - 类中定义的方法，直接放在原型上
```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
    this._address = "广州市"
  }

  // 普通的实例方法
  // 创建出来的对象进行访问
  // var p = new Person()
  // p.eating()
  eating() {
    console.log(this.name + " eating~")
  }

  running() {
    console.log(this.name + " running~")
  }
}
```

- 类的访问器方法
    - 讲对象的属性描述符时有讲过对象可以添加`setter`和`getter`函数的，那么类也是可以的
```js
class Person {
  // 类的访问器方法
  get address() {
    console.log("拦截访问操作")
    return this._address
  }

  set address(newAddress) {
    console.log("拦截设置操作")
    this._address = newAddress
  }
}
```

- 类的静态方法
    - 静态方法通常用于定义直接使用类来执行的方法，不需要有类的实例，使用static关键字来定义
```js
class Person {
  // 类的静态方法(类方法)
  // Person.createPerson()
  static randomPerson() {
    var nameIndex = Math.floor(Math.random() * names.length)
    var name = names[nameIndex]
    var age = Math.floor(Math.random() * 100)
    return new Person(name, age)
  }
}
```

- super关键字：
    - 注意：在子（派生）类的构造函数中使用this或者返回默认对象之前，必须先通过super调用父类的构造函数！
    - super的使用位置有三个：子类的构造函数、实例方法、静态方法
```js
// 调用 父对象/父类 的构造函数
super([arguments])

// 调用 父对象/父类 的方法
super.functionOnparent([arguments])
```

#### 继承内置类

```js
class HYArray extends Array {
  firstItem() {
    return this[0]
  }

  lastItem() {
    return this[this.length-1]
  }
}

var arr = new HYArray(1, 2, 3)
console.log(arr.firstItem())
console.log(arr.lastItem())
```

#### 类的混入 mixin
- JavaScript的类只支持单继承：也就是只能有一个父类
    - 在开发中我们需要在一个类中添加更多相似的功能时，可以使用混入（mixin）

```js
class Person {

}

function mixinRunner(BaseClass) {
  class NewClass extends BaseClass {
    running() {
      console.log("running~")
    }
  }
  return NewClass
}

function mixinEater(BaseClass) {
  return class extends BaseClass {
    eating() {
      console.log("eating~")
    }
  }
}

// 在JS中类只能有一个父类: 单继承
class Student extends Person {

}

var NewStudent = mixinEater(mixinRunner(Student))
var ns = new NewStudent()
ns.running()
ns.eating()
```

#### 阅读源码

1. ES6转ES5的代码
```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }

  eating() {
    console.log(this.name + " eating~")
  }
}
```
```js
// babel转换
"use strict";

function _classCallCheck(instance, Constructor) {
  if (!(instance instanceof Constructor)) {
    throw new TypeError("Cannot call a class as a function");
  }
}

function _defineProperties(target, props) {
  for (var i = 0; i < props.length; i++) {
    var descriptor = props[i];
    descriptor.enumerable = descriptor.enumerable || false;
    descriptor.configurable = true;
    if ("value" in descriptor) descriptor.writable = true;
    Object.defineProperty(target, descriptor.key, descriptor);
  }
}

function _createClass(Constructor, protoProps, staticProps) {
  if (protoProps) _defineProperties(Constructor.prototype, protoProps);
  if (staticProps) _defineProperties(Constructor, staticProps);
  return Constructor;
}

// /*#__PURE__*/ 纯函数
// webpack 压缩 tree-shaking
// 这个函数没副作用
var Person = /*#__PURE__*/ (function () {
  function Person(name, age) {
    this.name = name;
    this.age = age;
  }

  _createClass(Person, [
    {
      key: "eating",
      value: function eating() {
        console.log(this.name + " eating~");
      }
    }
  ]);

  return Person;
})();
```

2. ES6转ES5的继承
```js
class Person {
  constructor(name, age) {
    this.name = name
    this.age = age
  }

  running() {
    console.log(this.name + " running~")
  }

  static staticMethod() {

  }
}

class Student extends Person {
  constructor(name, age, sno) {
    super(name, age)
    this.sno = sno
  }

  studying() {
    console.log(this.name + " studying~")
  }
}
```
```js
// babel转换后的代码
"use strict";

function _typeof(obj) {
  "@babel/helpers - typeof";
  if (typeof Symbol === "function" && typeof Symbol.iterator === "symbol") {
    _typeof = function _typeof(obj) {
      return typeof obj;
    };
  } else {
    _typeof = function _typeof(obj) {
      return obj &&
        typeof Symbol === "function" &&
        obj.constructor === Symbol &&
        obj !== Symbol.prototype
        ? "symbol"
        : typeof obj;
    };
  }
  return _typeof(obj);
}

function _inherits(subClass, superClass) {
  if (typeof superClass !== "function" && superClass !== null) {
    throw new TypeError("Super expression must either be null or a function");
  }
  subClass.prototype = Object.create(superClass && superClass.prototype, {
    constructor: { value: subClass, writable: true, configurable: true }
  });
  // 目的静态方法的继承
  // Student.__proto__ = Person
  if (superClass) _setPrototypeOf(subClass, superClass);
}

// o: Student
// p: Person
// 静态方法的继承
function _setPrototypeOf(o, p) {
  _setPrototypeOf =
    Object.setPrototypeOf ||
    function _setPrototypeOf(o, p) {
      o.__proto__ = p;
      return o;
    };
  return _setPrototypeOf(o, p);
}

function _createSuper(Derived) {
  var hasNativeReflectConstruct = _isNativeReflectConstruct();
  return function _createSuperInternal() {
    var Super = _getPrototypeOf(Derived),
      result;
    if (hasNativeReflectConstruct) {
      var NewTarget = _getPrototypeOf(this).constructor;
      result = Reflect.construct(Super, arguments, NewTarget);
    } else {
      result = Super.apply(this, arguments);
    }
    return _possibleConstructorReturn(this, result);
  };
}

function _possibleConstructorReturn(self, call) {
  if (call && (_typeof(call) === "object" || typeof call === "function")) {
    return call;
  } else if (call !== void 0) {
    throw new TypeError(
      "Derived constructors may only return object or undefined"
    );
  }
  return _assertThisInitialized(self);
}

function _assertThisInitialized(self) {
  if (self === void 0) {
    throw new ReferenceError(
      "this hasn't been initialised - super() hasn't been called"
    );
  }
  return self;
}

function _isNativeReflectConstruct() {
  if (typeof Reflect === "undefined" || !Reflect.construct) return false;
  if (Reflect.construct.sham) return false;
  if (typeof Proxy === "function") return true;
  try {
    Boolean.prototype.valueOf.call(
      Reflect.construct(Boolean, [], function () {})
    );
    return true;
  } catch (e) {
    return false;
  }
}

function _getPrototypeOf(o) {
  _getPrototypeOf = Object.setPrototypeOf
    ? Object.getPrototypeOf
    : function _getPrototypeOf(o) {
        return o.__proto__ || Object.getPrototypeOf(o);
      };
  return _getPrototypeOf(o);
}

function _classCallCheck(instance, Constructor) {
  if (!(instance instanceof Constructor)) {
    throw new TypeError("Cannot call a class as a function");
  }
}

function _defineProperties(target, props) {
  for (var i = 0; i < props.length; i++) {
    var descriptor = props[i];
    descriptor.enumerable = descriptor.enumerable || false;
    descriptor.configurable = true;
    if ("value" in descriptor) descriptor.writable = true;
    Object.defineProperty(target, descriptor.key, descriptor);
  }
}

function _createClass(Constructor, protoProps, staticProps) {
  if (protoProps) _defineProperties(Constructor.prototype, protoProps);
  if (staticProps) _defineProperties(Constructor, staticProps);
  return Constructor;
}

var Person = /*#__PURE__*/ (function () {
  function Person(name, age) {
    _classCallCheck(this, Person);

    this.name = name;
    this.age = age;
  }

  _createClass(Person, [
    {
      key: "running",
      value: function running() {
        console.log(this.name + " running~");
      }
    }
  ]);

  return Person;
})();

var Student = /*#__PURE__*/ (function (_Person) {
  // 实现之前的寄生式继承的方法(静态方法的继承)
  _inherits(Student, _Person);

  var _super = _createSuper(Student);

  function Student(name, age, sno) {
    var _this;

    _classCallCheck(this, Student);

    // Person不能被当成一个函数去调用
    // Person.call(this, name, age)

    debugger;
    // 创建出来的对象 {name: , age: }
    _this = _super.call(this, name, age);
    _this.sno = sno;
    // {name: , age:, sno: }
    return _this;
  }

  _createClass(Student, [
    {
      key: "studying",
      value: function studying() {
        console.log(this.name + " studying~");
      }
    }
  ]);

  return Student;
})(Person);


var stu = new Student()

// Super: Person
// arguments: ["why", 18]
// NewTarget: Student
// 会通过Super创建出来一个实例, 但是这个实例的原型constructor指向的是NewTarget
// 会通过Person创建出来一个实例, 但是这个实例的原型constructor指向的Person
Reflect.construct(Super, arguments, NewTarget);
```

### JavaScript中的多态

- 面向对象的三大特性：封装、继承、多态

- 维基百科对多态的定义：多态（英语：polymorphism）指为不同数据类型的实体提供统一的接口，或使用一个单一的符号来表示多个不同的类型。
- 总结：不同的数据类型进行同一个操作，表现出不同的行为，就是多态的体现。
- 那么从上面的定义来看，JavaScript是一定存在多态的

```js
// 多态: 当对不同的数据类型执行同一个操作时, 如果表现出来的行为(形态)不一样, 那么就是多态的体现.
function calcArea(foo) {
  console.log(foo.getArea())
}

var obj1 = {
  name: "why",
  getArea: function() {
    return 1000
  }
}

class Person {
  getArea() {
    return 100
  }
}

var p = new Person()

calcArea(obj1)
calcArea(p)


// 也是多态的体现
function sum(m, n) {
  return m + n
}

sum(20, 30)
sum("abc", "cba")
```

## ES6-ES12新增

### ES6

#### 字面量的增强

字面量的增强主要包括下面几部分：
- 属性的简写：Property Shorthand
- 方法的简写：Method Shorthand
- 计算属性名：Computed Property Names

```js
var name = "why"
var age = 18

var obj = {
  // 1.property shorthand(属性的简写)
  name,
  age,

  // 2.method shorthand(方法的简写)
  foo: function() {
    console.log(this)
  },
  bar() {
    console.log(this)
  },
  baz: () => {
    console.log(this)
  },

  // 3.computed property name(计算属性名)
  [name + 123]: 'hehehehe'
}
```

#### 解构Destructuring

ES6中新增了一个从数组或对象中方便获取数据的方法，称之为解构Destructuring。
- 我们可以划分为：数组的解构和对象的解构。
- 数组的解构：
    - 基本解构过程
    - 顺序解构
    - 解构出数组
    - 默认值
```js
var names = ["abc", "cba", "nba"]
// var item1 = names[0]
// var item2 = names[1]
// var item3 = names[2]

// 对数组的解构: []
var [item1, item2, item3] = names
console.log(item1, item2, item3)

// 解构后面的元素
var [, , itemz] = names
console.log(itemz)

// 解构出一个元素,后面的元素放到一个新数组中
var [itemx, ...newNames] = names
console.log(itemx, newNames)

// 解构的默认值
var [itema, itemb, itemc, itemd = "aaa"] = names
console.log(itemd)
```
- 对象的解构：
    - 基本解构过程
    - 任意顺序
    - 重命名
    - 默认值
```js
var obj = {
  name: "why",
  age: 18,
  height: 1.88
}

// 对象的解构: {}
var { name, age, height } = obj
console.log(name, age, height)

var { age } = obj
console.log(age)

var { name: newName } = obj
console.log(newName)

var { address: newAddress = "广州市" } = obj
console.log(newAddress)


function foo(info) {
  console.log(info.name, info.age)
}

foo(obj)

function bar({name, age}) {
  console.log(name, age)
}

bar(obj)
```

