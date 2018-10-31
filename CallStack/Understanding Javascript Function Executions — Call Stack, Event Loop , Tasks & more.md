## Understanding Javascript Function Executions — Call Stack, Event Loop , Tasks & more

## 理解JavaScript中的函数执行 - 调用堆栈、事件循环、任务等

JavaScript的生态系统变得比以前复杂得多，并且在将来会继续如此。而构建现代网页应用所需的工具被WebpackBabel,ESLint,Mocha,Karma,Grunt...等等所囊括 - 我需要使用哪些工具以及这工具做什么？这个有个漫画：

![Javascript Fatigue — What it feels like to learn Javascript](https://cdn-images-1.medium.com/max/1600/1*1akEKXC95jhmIudAayITPA.png)

除此之外，每一个JavaScript开发者在深入使用任何框架以及库的之前，首先需要了解其基础知识，知道在底层其是如何实现的。大部分JavaScript开发者都听说过V8,但是很多可能并不知道其是什么以及做什么。在我职业生涯的第一年，作为一名开发者，对于这些花哨的术语也不太了解，因为更加重要的是首先完成工作。

JavaScript是一个单线程并发的语言，这意味它只可以同时处理一个任务或一段代码。它具有一个单独的调用堆栈，它与堆、队列等其他部分一起构成JavaScript并发模型(V8中的实现)。

![javascript concurrency](https://cdn-images-1.medium.com/max/1600/1*ZSFHnq9iMHIApVLcgwczPQ.png)

1. 调用栈(Call Stack)：它是一个记录函数调用的数据结构，记录下程序执行到那里。当我们调用一个函数，就是向调用栈push入一个函数，而当函数执行完毕，return后，该函数将从调用栈pop出来。

![call stack](https://cdn-images-1.medium.com/max/1600/1*E3zTWtEOiDWw7d0n7Vp-mA.gif)

2. 堆(Heap)：对象在堆中分配，即大部分是非结构化的内存区域。所有变量和对象的内存分配都在这里发生。

3. 队列(Queue)：一个JavaScript运行时包含一个消息队列，该消息队列就是一组需要被处理的消息以及相关的回调。当调用栈为空的时候，将从队列中取一个消息作为调用栈的初始帧开始执行。当调用栈再次为空时，表示该消息处理完毕。简言之，这些消息是由外部异步创建的。

## Event Loop


> Browser Web APIs- threads created by browser implemented in C++ to handle async events like DOM events, http request, setTimeout, etc.
 
> 浏览器WebAPI——由C++实现的浏览器创建的线程，处理诸如DOM事件、HTTP请求、StimeTimeUT等异步事件。

![Event Loop](https://cdn-images-1.medium.com/max/1600/1*-MMBHKy_ZxCrouecRqvsBg.png)

* 3 Any of the WebAPI pushes the callback onto this queue when it`s done executing.
* 4 The `Event Loop` now is responsible for the execution of these callbacks in the queue and pushing it in the stack,when it is empty.
* Event loop basic job is to look both at the stack and the task queue, pushing the first thing on the queue to the stack when it see stack as empty. 
*  Each message or callback is processed completely before any other message is processed.