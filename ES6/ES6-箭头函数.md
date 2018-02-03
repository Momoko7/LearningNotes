## ES6学习笔记-Arrow Function 箭头函数
### 1.基本用法
```javascript
var f = () => 5;
// 等同于
var f = function () { return 5 };
```
```javascript
var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```
```javascript
//如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。
var sum = (num1, num2) => { return num1 + num2; }
//由于大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。
var getTempItem = id => ({ id: id, name: "Temp" });
```
```javascript
/*结合变量解构*/
var sum = ({num1, num2}) => num1+num2
```

### 2.注意this指向
- 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。
- 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
- 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用Rest参数代替。
- 不可以使用yield命令，因此箭头函数不能用作Generator函数。


>**this指向的是外层函数**
并不是因为箭头函数内部有绑定this的机制，实际原因是箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。
正是因为它没有this，所以也就不能用作构造函数。
同样，arguments在箭头函数之中也是不存在的，指向外层函数的参数。



