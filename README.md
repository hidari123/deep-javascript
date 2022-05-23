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

![avatar](/image//01/%E6%B5%8F%E8%A7%88%E5%99%A8%E6%B8%B2%E6%9F%93%E8%BF%87%E7%A8%8B.png)

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

![avatar](/image/01/v8%E5%BC%95%E6%93%8E%E5%8E%9F%E7%90%86.png)

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

![avatar](/image/01/%E5%A0%86%E5%86%85%E5%AD%98.png)

2. 执行上下文栈（调用栈）

js引擎内部有一个执行上下文栈（Execution Context Stack，简称ECS），它是用于执行代码的调用栈。
那么现在它要执行谁呢？执行的是全局的代码块：
 - 全局的代码块为了执行会构建一个 Global Execution Context（GEC）；
 - GEC会 被放入到ECS中 执行；
 - GEC被放入到ECS中里面包含两部分内容：
    - 第一部分：在代码执行前，在parser转成AST的过程中，会将全局定义的变量、函数等加入到GlobalObject中，但是并不会赋值；
        - 这个过程也称之为变量的作用域提升（hoisting）
    - 第二部分：在代码执行中，对变量赋值，或者执行其他的函数
![avatar](/image/01/GEC%E8%A2%AB%E6%94%BE%E5%85%A5%E5%88%B0ECS%E4%B8%AD.png)
![avatar](/image/01/GEC%E5%BC%80%E5%A7%8B%E6%89%A7%E8%A1%8C%E4%BB%A3%E7%A0%81.png)