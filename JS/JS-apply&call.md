# JS-关于apply与call的用法

> #### 应用场景 _（劫持别人的方法）_
> ##### call和apply都是是为了动态改变this而出现的，当一个object没有某个方法，但是其他的有，我们可以借助call或apply用其它对象的方法来操作。
> call和apply二者的作用完全一样，只是接受参数的方式不太一样。

## 1.方法定义
* **apply** _（最多接受两个参数）_
  > `Function.apply(obj,args)`方法能接收两个参数：
    obj：这个对象将代替Function类里this对象
    args：这个是数组，apply方法把这个集合中的元素作为参数传递给被调用的函数。
* **call** _（可以接收多个参数，使用`,`隔开）_
  > call方法与apply方法的第一个参数是一样的，第二个参数是参数列表
* 非严格模式下当我们没有传参或第一个参数传递为null或undefined时，函数体内的this会**指向默认的宿主对象**，在浏览器中则是window
    ```javascript
    var test = function(){
      console.log(this===window);
    }
    test.apply(null);      //true
    test.call(null);       //true
    test.apply(undefined); //true
    test.call(undefined);  //true
    ```
   
## 2.看些栗子
```javascript
window.color = 'red';
document.color = 'yellow';
var s1 = {color: 'blue' };
function changeColor(){
    this.color = 'black'
    console.log(this.color);
}

changeColor.call();         //red (默认传递参数父级作用域window)
changeColor.call(window);   //red
changeColor.call(document); //yellow
changeColor.call(this);     //red
changeColor.call(s1);       //blue
```
看看结果感受感受先... next to usage
## 3.用法
### 1）“劫持”别人的方法
  ```javascript
var foo = {
  name:"mingming",
  logName:function(){
    console.log(this.name);
  }
}
var bar={
  name:"xiaowang"
};
foo.logName.call(bar);//xiaowang
```
 ```javascript
var foo = {
  name:"mingming",
  logName:function(){
	this.color = 'red'
    console.log(this);
  }
}
var bar={
  name:"xiaowang",
  color:'green',
  age:12
};
foo.logName.call(bar);
/*结果为
{name: "xiaowang", age: 12, color: "red"}
* */
```
由此，此时bar方法里没有`logName`方法，通过call方法可以将foo的`logName`方法‘纳为己用’，并且该方法中的this会直接指向bar对象。
### 2）实现继承
```javascript
function Animal(name){   
  this.name = name;   
  this.showName = function(){   
    console.log(this.name);   
  }   
}
function Cat(name){  
  Animal.call(this, name);  
}
var cat = new Cat("Black Cat");   

cat.showName();   //Black Cat
```
```javascript
function Animal(name){   
  this.name = name;  
  this.age = 1;   //定值
  this.showName = function(){   
    console.log(this);  //直接打印this 
  }   
}   
function Cat(name){  
  this.age = 2   
  Animal.call(this, name);  //！注意，这里的age也会直接被Animal里的age给覆盖
}   
 
var cat = new Cat("Black Cat");   
cat.showName(); 
/*结果为
{age: 1, name: "Black Cat", showName: ƒ}
* */
```
### 3）其他用法
+ **类数组** 
  这里把符合以下条件的对象称为类数组
  + 具有length属性
  + 按索引方式存储数据
  + 但是不具有数组的push,pop等方法
   常见类数组有arguments,NodeList
      
      ```javascript
    (function(){    
        Array.prototype.push.call(arguments,3,4);    
        console.log(arguments);//[1, 2, 3, 4]
    })(1,2)
       ```
  



> 参考： [文章一](https://www.cnblogs.com/faithZZZ/p/6999327.html)
  参考： [文章二](http://blog.csdn.net/ganyingxie123456/article/details/70855586)