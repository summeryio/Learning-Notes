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



##### 数值范围

isFinite()   确定一个数是不是位于最 小和最大的数值之间



##### NaN

isNaN() // 接受一个参数，转换为数值，不能转的返回true

有 0 除以 0 才会返回 NaN，正数除以 0 返回 Infinity，负数除以 0 返回-Infinity



##### 数值转换

###### Number()

1. 如果是 Boolean 值，true 和 false 将分别被转换为 1 和 0。 
2. 如果是数字值，只是简单的传入和返回。
3.  如果是 null 值，返回 0。 
4. 如果是 undefined，返回 NaN。
5. 空字符串 返回0



###### parseInt()

函数提供第二个参数，即转换时使用的基数（多少进制）

在使用时，需要明确指定基数

```
console.log(parseInt('0xAF', 16)); // 175
console.log(parseInt('AF', 16)); // 175
console.log(parseInt('AF')); // NaN
```

###### parseFloat()

1. 始终会忽略前面的0
2. 只解析十进制值，没有第二个参数
3. 多个小数点，只保留最前面的小数点

```
console.log(parseFloat('1232dwad')); // 1232
console.log(parseFloat('0xAF')); // 0
console.log(parseFloat('12.25.23')); // 12.25
console.log(parseFloat('0908.2')); // 908.2
console.log(parseFloat('3.125e7')); // 31250000
```



##### String 类型

null  undefined 没有 toString() 方法，会报错



###### 在调用数值的 toString()方法时，可 以传递一个参数(进制基数)：输出数值的进制值

```
var num = 10;
alert(num.toString()); // "10"
alert(num.toString(2)); // "1010"
alert(num.toString(8)); // "12"
alert(num.toString(10)); // "10"
alert(num.toString(16)); // "a" 
```



###### 在不知道要转换的值是不是 null 或 undefined 的情况下，还可以使用转型函数 String()，这个 函数能够将任何类型的值转换为字符串

1. 如果值有 toString()方法，则调用该方法（没有参数）并返回相应的结果； 
2.  如果值是 null，则返回"null"； 
3.  如果值是 undefined，则返回"undefined"。

```
var value1 = 10;
var value2 = true;
var value3 = null;
var value4;
alert(String(value1)); // "10"
alert(String(value2)); // "true"
alert(String(value3)); // "null"
alert(String(value4)); // "undefined" 
```



##### Object 类型 (53)



------

##### 一元操作符 (54)

###### 前置递增/递减  (变量的值都是在语句被求值以前改变的)

```
var num = 2
var num2 = 20
var num3 = --num + num2 // 这里num = 1
var num4 = num + num2

console.log(num3); // 21
console.log(num4); // 21
```

###### 注：当语句还包含其他操作时，就会有区别

###### 前置递增/递减  (变量的值都是在语句被求值之后改变的)

```
var num = 2
var num2 = 20
var num3 = num-- + num2 // 这里num = 2，使用了原始值
var num4 = num + num2 // 这里num = 1，使用了递减后的值

console.log(num3); // 22
console.log(num4); // 21
```



###### 不仅适用于整数，还可以用于字符串、布尔值、浮 点数值和对象

```
var s1 = "2";
var s2 = "z";
var b = false;
var f = 1.1;
var o = {
 valueOf: function() {
 return -1;
 }
};
s1++; // 值变成数值 3
s2++; // 值变成 NaN
b++; // 值变成数值 1
f--; // 值变成 0.10000000000000009（由于浮点舍入错误所致）
o--; // 值变成数值-2 
```





##### 一元加和减操作符(56)

```
// +
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = {
 valueOf: function() {
 return -1;
 }
};
s1 = +s1; // 值变成数值 1
s2 = +s2; // 值变成数值 1.1
s3 = +s3; // 值变成 NaN
b = +b; // 值变成数值 0
f = +f; // 值未变，仍然是 1.1
o = +o; // 值变成数值-1 
```

```
// -
var s1 = "01";
var s2 = "1.1";
var s3 = "z";
var b = false;
var f = 1.1;
var o = {
 valueOf: function() {
 return -1;
 }
};
s1 = -s1; // 值变成了数值-1
s2 = -s2; // 值变成了数值-1.1
s3 = -s3; // 值变成了 NaN
b = -b; // 值变成了数值 0
f = -f; // 变成了-1.1
o = -o; // 值变成了数值 1 
```



------



#### 布尔操作符(62)

##### 逻辑非 ! 

###### 首先会将它的操作数转换为一个布尔值，然后再 对其求反

```
// 如果操作数是一个对象
var n = {age: 100}
console.log(!n); // false
```

```
// 如果操作数是任意非 0 数值（包括 Infinity），返回 false；
var n = Number.MAX_VALUE + Number.MAX_VALUE
console.log(!n); // false
```

###### !!  得到这个值真正对应的布尔值，与使用Boolean() 相同

```
alert(!!"blue"); //true
alert(!!0); //false
alert(!!NaN); //false
alert(!!""); //false
alert(!!12345); //true 
```



##### 逻辑与 &&

###### 不能在逻辑与操作中使用未定义的值

```
var found = true
var result = (found && someUndefinedVariable) // 报错 someUndefinedVariable is not defined
console.log(res); // 这行不会执行
```

```
var found = false
var result = (found && someUndefinedVariable) // 不会报错
console.log(res);
```



------

#### 乘性操作符

##### 乘法

1. 非数值的情况下执行自动类型转换，如果某个操作数不是数值，后台会先使用 Number()转型函数将其转换为数值
2. 有一个操作数是NaN，结果是NaN



##### 除法

1. 规则同上
2. 0 / 0   // NaN



##### 加法

1. 如果两个操作数都是字符串，则将第二个操作数与第一个操作数拼接起来； 
2. 如果只有一个操作数是字符串，则将另一个操作数转换为字符串，然后再将两个字符串拼接 起来。

```
var result = '20' + 10
console.log(result); // '2010'
```



##### 减法

1. 如果有一个操作数是字符串、布尔值、null 或 undefined，则先在后台调用 Number()函数将 其转换为数值，然后再根据前面的规则执行减法计算。如果转换的结果是 NaN，则减法的结果 就是 NaN；

```
var result = '20' - 10
console.log(result); // 10
```

```
var result = '20' - undefined
console.log(result); // NaN
```





------

#### 关系操作符

##### <  >  <=  >=

1. 如果两个操作数都是字符串，则比较两个字符串对应的字符编码值
2. 如果一个操作数是数值，则将另一个操作数转换为一个数值，然后执行数值比较。
3. 任何操作数与 NaN 进行 关系比较，结果都是 false



##### ==   !=

1. null == undefined  // true
2. 要比较相等性之前，不能将 null 和 undefined 转换成其他任何值；null == 0 // false
3. 如果有一个操作数是 NaN，则相等操作符返回 false，而不相等操作符返回 true
4. NaN != NaN
5. 如果两个操作数都是对象，则比较它们是不是同一个对象



##### ===   !==

1. null === undefined  // false





------

#### 条件语句

##### do-while

```
// 至少会被执行一次
var i = 20
do {
i += 2
console.log(i); // 22
} while (i < 10);
```



##### while

```
// 条件不成立，永远不会执行
var i = 20
while(i < 10) {
i += 2
console.log(i);
}
```



##### for

###### 在循环内部定义的变量也可以在外部访问到

```
var count = 10
for (var i = 0; i < count; i ++) {
	console.log(i);
}
console.log('i: ', i);
```

###### 将 （的初始化表达式、控制表达式和循环后表达式） 全部 省略，就会创建一个无限循环

```
for (;;) { // 无限循环
 doSomething();
} 
```

###### 只给出控制表达式实际上就把 for 循环转换成了 while 循环

```
// 这里等同于第一个例子
var count = 10
var i = 0
for (; i < count; ) {
  console.log(i);
  i++
}
```



##### for-in

在使用 for-in 循环之前，先检测确认该对象的值不是 null 或 undefined

```
var obj = {name: 'summer', age: 20, test: null}
var animal = null

if (obj) {
    for (var key in obj) {
    	console.log(obj[key]);
    }
}
```



##### break和continue语句

###### break 会立即退出循环，强制继续执行循环后面的语句

```
var num = 0
for (var i = 1; i < 10; i ++) {
    if (i % 5 == 0) {
    	break;
    }
    num++ // num = 4 时就退出循环了
}
console.log(num); // 4
```



###### continue  也是立即退出循环，但退出循环后会从循环的顶 部继续执行

```
var num = 0
for (var i = 1; i < 10; i ++) {
    if (i % 5 == 0) {
        continue;
    }
    num++
}
console.log(num); // 8，continue导致少循环了一次
```



###### 使用 label 语句，与 break / continue 联用

```
var num = 0

outermost:
for (var i = 0; i < 10; i ++) {
    for (var j = 0; j < 10; j ++) {
        if (i == 5 && j == 5) {
            break outermost // 返回到 outermost
        }
        num++
    }
}
console.log(num); // 55
```

```
var num = 0

outermost:
for (var i = 0; i < 10; i ++) {
    for (var j = 0; j < 10; j ++) {
        if (i == 5 && j == 5) {
            continue outermost // 退出内部循环，执行外部循环
        }
        num++
    }
}
console.log(num); // 95
```

