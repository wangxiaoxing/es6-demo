# es6-demo

1.let const var
 let:
 只在let命令所在的代码块内有效；不存在变量提升，使用前先声明；不允许重复声明；增加了块级作用域。
 
Const:
声明常量，一旦声明，常量的值就不能改变，对常量重新赋值不会报错，只会默默失败；
只在声明的块级作用域内有效；不存在变量提升；不允许重复声明；

var 和function命令声明的全局变量，属于全局对象的属性；let const class命令声明的全局变量，不属于全局对象的属性。

2.变量的结构赋值

解构：按照一定模式，从数组和对象中提取值，对变量进行赋值。
解构只能用于数组或对象。其他原始类型的值都可以转为相应的对象，但是，undefined和null不能转为对象。
不能使用圆括号的情况：
（1）变量声明语句中，模式不能带有圆括号；
 （2）函数参数中，模式不能带有圆括号；
（3）不能将整个模式，或嵌套模式中的一层，放在圆括号之中。
可以使用圆括号的情况：
赋值语句的非模式部分，可以使用圆括号。
用途：
(1)交换变量的值[x,y]=[y,x];
(2)从函数返回多个值；
(3)函数参数的定义；
(4)提取json数据；
(5)函数参数的默认值；
(6)遍历Map结构
(7)输入模块的指定方法


3.字符串的扩展

1.加强了对Unicode码点大于0xFFFF的字符的支持。
2.includes().startsWith().endsWith(),repeat()
3.模板字符串
4.String.raw():充当模板字符串的处理函数，返回一个斜杠都被转义的字符串，对应于替换变量后的模板字符串。

4.数值的扩展

1.Number.isFinite()   检查数值是否非无穷
   Number.isNaN()    检查数值是否为NaN
 与传统的全局方法isFinite()、isNaN()的区别：
 传统方法先调用Number()将非数值的值转为数值，再进行判断；新方法只对数值有效，非数值一律返回false.
2.Number.parseInt() Number.parseFloat()与全局方法parseInt()、parseFloat()行为一致
3.Number.isInteger()判断一个值是否为整数，3和3.0被视为同一个值
   Number.isSafeInteger()判断一个整数是否落在js能准确表示的整数范围内。

5.Math对象的扩展

Math.trunc() 去除一个数的小数部分，返回整数部分。
Math.sign()   判断一个数是正数、负数还是零。NaN返回NaN;


6.数组的扩展

Array.from()  将类数组对象和可遍历对象转为真正的数组=Array.prototype.slice.call(obj);
Array.of()  将一组值，转换为数组。
数组实例的find()  找出第一个符合条件的数组成员，返回该成员，没有符合条件的返回undefined
[1, 5, 10, 15].find(function(value, index, arr) {
  return value > 9;
}) // 10
数组实例的 findIndex 方法的用法与 find 方法非常类似，返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回 -1。
[1, 5, 10, 15].findIndex(function(value, index, arr) {
  return value > 9;
}) // 2
数组实例的fill()
['a', 'b', 'c'].fill(7)
// [7, 7, 7]
第二第三参数用于指定填充的起始位置和结束位置。
['a', 'b', 'c'].fill(7, 1, 2)
// ['a', 7, 'c']
数组实例的entries().keys().values()
返回一个遍历器，可以用for of 遍历返回的结果。entries()是对键值对的遍历。
for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
数组实例的includes()
返回一个布尔值，表示某个数组是否包含给定的值。第二个参数表示搜索的起始位置，默认为0
Array.observe().Array.unobserve() 监听（取消监听）数组的变化，指定回调函数。

7.对象的扩展

ES6允许直接写入变量和函数，作为对象的属性和方法，书写更加简洁

function getPoint() {
  var x = 1;
  var y = 10;

  return {x, y};
}

getPoint()
// {x:1, y:10}
Object.is()
比较两个值是否严格相等，与===的行为基本一致，但是+0不等于-0，0等于+0,0不等于-0；NaN等于自身。
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
Object.assign()
将源对象的所有可枚举对象复制到目标对象，第一个参数是目标对象，后面的参数都是源对象。
作用：为对象添加属性；为对象添加方法；克隆对象(不能克隆他继承的值)；合并多个对象
proto属性，Object.setPrototypeOf(),Object.getPrototypeOf()
// es6的写法

var obj = {
  __proto__: someOtherObj,
  method: function() { ... }
}

// es5的写法

var obj = Object.create(someOtherObj);
obj.method = function() { ... }
Object.setPrototypeOf()：设置一个对象的prototype对象
Object.getPrototypeOf()：读取一个对象的prototype对象
Object.observe(),Object.unobserve():监听对象及数组的变化，一旦监听对象发生变化，就会触发回调函数。

8.Symbol  

保证每个属性名字都是独一无二的，凡是属性名属于Symbol类型，就是独一无二的，可以保证不会与其他属性名产生冲突。相同参数的 Symbol 函数的返回值是不相等的。
对象的内部，使用 Symbol 值定义属性时，Symbol 值必须放在方括号之中。 
Symbol 作为属性名，该属性不会出现在 for...in、for...of 循环中，也不会被Object.keys()、Object.getOwnPropertyNames()返回。
Object.getOwnPropertySymbols 方法，可以获取指定对象的所有 Symbol 属性名。

9.函数的扩展：

函数参数的默认值；

