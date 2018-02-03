# ES6 Rest参数
> #### MDN概述：The rest parameter syntax allows us to represent an indefinite number of arguments as an array.

#### Rest参数接收函数的多余参数，组成一个数组，放在形参的最后，形式如下：
```javascript
function fun(a, b, ...theArgs) {
    // ...
}
```

### Rest参数和arguments对象的区别
+ rest参数只包括那些没有给出名称的参数，arguments包含所有参数；
+ arguments对象不是真正的array(类数组)，而rest参数是Array的实例，可以直接应用sort, map, forEach, pop等方法；
+ arguments对象拥有一些自己额外的功能（callee）。
+ 注意，rest参数之后不能再有其它参数（即，只能是最后一个参数），否则会报错。
