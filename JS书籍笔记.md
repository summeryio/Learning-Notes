#### JavaScript 高级程序设计



##### 一个完整的 JavaScript 实现应该由下列三 个不同的部分组成

 核心（ECMAScript） // 提供核心语言功能

 文档对象模型（DOM） Document Object Model  // 提供访问和操作网页内容的方法和接口

 浏览器对象模型（BOM）Browser Object Model  // 提供与浏览器交互的方法和接口



```
使用分号

if (test)
 alert(test); // 有效但容易出错，不要使用
if (test){ // 推荐使用
 alert(test);
} 
```



##### Null 类型

null 值表 示一个空对象指针

```
var test = null
console.log(typeof test); // 'object'
```



如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为 null 而不是其他值

```
if (car != null){
 // 对 car 对象执行某些操作
} 
```



##### JS布尔值(Boolean)转换规则

https://blog.csdn.net/qq_34412985/article/details/104620959

