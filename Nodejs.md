# Node.js
简单的说 Node.js 就是运行在服务端的 JavaScript。

Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。

Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。


什么是[[异步编程]]什么是[[同步编程]]？

 Nodejs的异步编程的直接体现就是 #回调 ,异步编程依托于回调来实现，并不能说回调程序就异步化了。
 
 Node所有的API都支持回调函数。
 
 回调函数一般作为最后一个参数出现：
 
 ```
 function foo1(name, age, callback) { } 
 function foo2(value, callback1, callback2) { }
 ```