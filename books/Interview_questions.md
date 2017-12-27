1. 下面代码会输出什么？
```js
var y = 1;
if(function f(){}){
    y += typeof f;
}
console.log(y);  
```
答案： 1undefined   

解析：
if条件语句用eval进行解析，所以eval(function f(){})返回function f(){}，故if条件表达式里值为true;
if语句代码在运行时执行，所以typeof f为undefined.
看个类似的例子： 
```js
var y = 1;
if(1){
    eval(function f(){})
    y += typeof f;
}
console.log(y);  //1undefined
```
最后看正常的例子：
```js
var k = 1;
if(1){
    function foo(){}
    k += typeof foo;
}
console.log(k);  //1function
```
2. 闭包（？？？）

闭包是另一个函数（成为父函数）中定义的函数，可以访问在父函数作用域中声明和定义的变量。
闭包可以访问三个范围内的变量：
- 变量在自己的范围内声明
- 在父函数范围中声明的变量
- 在全局命名空间中声明的变量
示例如下：
```js
var globalVar = 'abc';

(function outerFunction(outerArg){
    var outerFuncVar = 'x';  
    (function innerFunction(innerArg){
        var innerFuncVar = 'y'; 
        console.log(
            "outerArg = " + outerArg + "\n" +                //7
            "outerFuncVar = " + outerFuncVar + "\n" +       //x
            "innerArg = " + innerArg + "\n" +               //5
            "innerFuncVar = " + innerFuncVar + "\n" +       //y
            "globalVar = " + globalVar                      //abc
        )
    })(5)
})(7);
```
```js
var name = 'World!';
(function(){
if(typeof name === 'undefined'){
    var name = 'jack';
    console.log('Goodbye ' + name);
}else{
    console.log('Hello ' + name);
}
})();

//  Goodbye jack
```
```js
var name = 'World!';
(function(){
    if(typeof name === 'undefined'){
        console.log('Goodbye ' + name); 
    }else{
        console.log('Hello ' + name); 
    }
})();

//Hello world!
```
3. 写一个mul函数，当调用时将产生下面的输出：  
console.log(mul(2)(3)(4)); // output : 24   
console.log(mul(4)(3)(4)); // output : 48  
```js
function mul(x){
    return function(y){
        return function(z){
            return x * y * z;
        }
    }
}
```
4.



