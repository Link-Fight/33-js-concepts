# How JavaScript works: an overview of the engine, the runtime, and the call stack

   对于V8引擎，大多数人知道JavaScript是单线程的或者说它是使用回调队列的。

   ![v8](https://cdn-images-1.medium.com/max/1600/1*OnH_DlbNAPvB9KLxUCyMsA.png)

   这v8引擎主要包括两大部分：
   1. Memory Heap - 内存分配的地方
   2. Call Stack - 代码执行是存放调用帧的地方

   ## 运行时

   有些api几乎每一个JavaScript开发者都会用到，但是这些api是由浏览器提供的，而不是v8引擎。

   ![runtime](https://cdn-images-1.medium.com/max/1600/1*4lHHyfEhVB0LnQ3HlhSs8g.png)

   我们把这些api称为`Web APIs`,是由浏览器提供的，例如：DOM,AJAX,setTimeout 等

   ## 调用堆栈

   因为JavaScript是单线程的，这意味着只有一个调用堆栈。因此同一时间只能做一件事。

   调用栈是一种能够记录程序执行位置的数据结构。当我们调用一个函数，就是把函数推入到调用栈中。当函数执行完毕，就是从调用栈中把其推出来。

   eg:
   ```js
   function multiply(x, y) {
    return x * y;
    }
    function printSquare(x) {
      var s = multiply(x, x);
      console.log(s);
    }
    printSquare(5);
   ```

   ![eg](https://cdn-images-1.medium.com/max/1600/1*Yp1KOt_UJ47HChmS9y7KXw.png)

   每次进入调用堆栈都会创建一个调用帧。

   ## 并发和事件循环