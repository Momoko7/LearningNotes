# 关于变量声明
```javascript
    var a ;             //①声明
    function f1() {
        console.log(a)
        a = 2            //a在①处被声明
        console.log(a)
    }
    f1()
    console.log(a)
    /*结果：
    undefined
    2
    2
    */
```
```javascript
    var a ;    
    function f1() {
        console.log(a)
        var a = 2        //重新声明并赋值
        console.log(a)
    }
    f1()
    console.log(a)
    /*结果
    undefined
    2
    undefined       //这里的值来自于当前作用域
    */
```
```javascript
    var a = 0;
    function f1() {
        console.log(a)
        var a;          //重新声明但未赋值
        console.log(a)
    }
    f1()
    console.log(a)
    /*结果
    undefined
    undefined
    2
    */
```
### 
