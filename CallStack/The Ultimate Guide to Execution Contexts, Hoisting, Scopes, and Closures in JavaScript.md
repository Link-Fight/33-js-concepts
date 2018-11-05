## The Ultimate Guide to Execution Contexts, Hoisting, Scopes, and Closures in JavaScript

对于JavaScript引擎来说，执行代码需要创建执行上下文(Execution Context ),执行全局代码会创建全局执行上下文。执行函数调用的时候，就会创建函数执行上下文。

而一个执行上下文会包括两部分，`Creation`(创建)和`Execution`(执行)。

对于全局执行上下文，在`Creation`阶段，会做：

1. 创建全局对象
2. 创建`this`对象
3. 为`var`声明的变量以及函数声明分配内存
4. 为声明的变量赋予默认值`undefined`以及分配函数对应的内存

对于函数执行上下文，在`Creation`阶段，会做：

~~1.Create a global object~~
1. 创建`arguments`对象 
2. 创建`this`对象 
3. 为`var`声明的变量以及函数声明分配内存
4. 为声明的变量赋予默认值`undefined`以及分配函数对应的内存

