## 考点： forEach和map
```js
['1a','b2','3c'].forEach(function(e){
    console.log(parseInt(e));
})
```
```js
['1a','b2','3c'].map(parseInt)
```
## 考点： var, let 
var
```js
var a = function(){
    console.log(i);  // undefined
    var i = 1;
    console.log(i);     // 1
}
a();
```
let
```js
var a = function(){
    console.log(i);
    let i = 1;
    console.log(i);
}
a();
```
```js
let i = 2;
var a = function(){
    console.log(i);
    let i = 1;
}
```

## this
```js
function A(){
    this.name = 'test1';
    this.showName = function(){
        console.log(this.name);
    }
}
function B(){
    this.name = 'test2';
}
var a = new A();
var b = new B();
console.log(a.name);    // test1
console.log(b.name);    // test2
a.showName();  // test1
a.showName.call(b);   // test2
a.name = 'test3';
a.showName().call(b);  // test2
```

## position几种定位方式及区别

## session, cookie, localstorage, sessionstorage区别

## 实现两栏布局，左边固定宽度，右边自适应。

## es6新增特性

## 什么是同源策略？跨域解决方式有哪几种？

## 前端性能优化

## 闭包的应用场景；闭包使用完了没有垃圾回收为什么没有内存泄漏；使用闭包时如何释放引用

## js如何实现继承（es5和es6）