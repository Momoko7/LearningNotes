# 三个点（...）
> ### 作用
> #### 扩展运算符允许一个表达式在期望多个参数（用于函数调用）或多个元素（用于数组字面量）或多个变量（用于解构赋值）的位置扩展。
> #### 好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

## use it

### 1.将一个数组放入另一个数组中
```javascript
var middle = [3, 4];
var arr = [1, 2, ...middle, 5, 6];
console.log(arr);
// [1, 2, 3, 4, 5, 6]
```

### 2.复制数组（代替slice）
```javascript
var arr = ['a', 'b', 'c'];
var arr2 = [...arr];
console.log(arr2);
// ['a', 'b', 'c']
```
arr数组中的元素扩展成为单独元素被分配到arr2中。现在可以随意改变arr2数组，且都不会对源数组arr产生影响
> 注意：要得到新的数组，不能使用等号直接赋值(除非对你需求不影响)，这里涉及js的深拷贝与浅拷贝。详情百度。

### 3.拼接数组（代替contact）
```javascript
var arr1 = ['a', 'b', 'c'];
var arr2 = ['d', 'e', 'f'];
arr = [...arr1, ...arr2];
console.log(arr);
// ['a', 'b', 'c', 'd', 'e', 'f']
```
### 4.Math
##### 也可以使用math函数连同扩展运算符。如这个例子中，将使用Math.max()返回数组中的最大值。
在没有扩展运算符，在数组上使用Math.max()最容易方法就是使用.apply()。
```javascript
var arr = [2, 4, 8, 6, 0];
function myMax(arr) {
  return Math.max.apply(null, arr);  //传入为空 默认指向myMax
}
console.log(myMax(arr)); // 8
```
使用扩展运算符做同样事情。只需要两行代码就可以做到同样效果。
```javascript
var arr = [2, 4, 8, 6, 0];
var max = Math.max(...arr);
console.log(max);   // 8
```

### 5.字符串转数组(代替)
##### 使用扩展运算符将字符串转换为数组。
```javascript
var str = "hello";
var chars = [...str];
console.log(chars); 
// ['h', 'e',' l',' l', 'o']
```




> ### 总而言之，一切需要将数组中的元素当做参数来使用的情况都可以使用这个扩展运算符，并且传入的参数依然是被保存在arguments类数组里。当然前提是要支持ES6语法。