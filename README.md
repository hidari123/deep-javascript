<!--
 * @Author: hidari
 * @Date: 2022-05-23 10:37:10
 * @LastEditors: hidari 
 * @LastEditTime: 2022-05-24 17:27:48
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
