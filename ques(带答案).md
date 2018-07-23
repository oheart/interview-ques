## 考点： forEach和map
```js
['1a','b2','3c'].forEach(function(e){
    console.log(parseInt(e));
})
```
```js
['1a','b2','3c'].map(parseInt)
```
## 以下代码会输出什么？
var
```js
var a = function(){
    console.log(i);  
    var i = 1;
    console.log(i);    
}
a();
```
答案：  undefined， 1   
考点： var声明的变量提升 

let
```js
var a = function(){
    console.log(i);
    let i = 1;
    console.log(i);
}
a();
```
答案： Uncaught ReferenceError: i is not defined  
考点： let定义没有变量提升
```js
let i = 2;
var a = function(){
    console.log(i);
    let i = 1;
}
a();
```
答案：Uncaught ReferenceError: i is not defined  
考点： let(i的作用域问题)，只要块级作用域内存在let命令，它所声明的变量就“绑定”这个区域，不再受外部的影响。let声明的变量只在它所在的代码块有效。
## 以下代码会输出什么？
```js
var name = 'outername';
var object = {
    name: 'innername',
    sayName: function(){
        return this.name;
    },
    sayName2: () => {
        return this.name;
    }
}
object.sayName();
object.sayName2();
```
答案： innername   outername  
考点： this指向和箭头函数

## 以下会输出什么？如何改进？ 
```js
var data = [];
for(var i = 0; i < 3; i++){
    data[i] = function(){
        console.log(i);
    }
}
data[0]();
data[1]();
data[2]();
```
答案： 输出3, 3, 3; 正常应该输出0，1，2；  
考点：闭包和es6新增块级作用域  
改进：   
- IIFE立即执行函数
```js
var data = [];
for(let i = 0; i < 3; i++){
    (function(j){
            data[j] = function(){
            console.log(j);
        }
    })(i);  
}
data[0]();
data[1]();
data[2]();
```
- let
```js
var data = [];
for(let i = 0; i < 3; i++){
    data[i] = function(){
        console.log(i);
    }
}
data[0]();
data[1]();
data[2]();
```

## DOM结构为
```HTML
<ul>
    <li> 菜单1</li>
    <li> 菜单2</li>
    <li> 菜单3</li>
    <li> 菜单4</li>
    <li> 菜单5</li>
    ...
</ul>
```
请为上面的每个li节点绑定一个点击事件，li的节点数量会随时变化，请写出事件绑定代码（可以用使用jQuery）.  

答案：   
$('ul').on('click', 'li', function () {})   
$('ul').delegate('click', 'li', function () {})    
考点：jquery动态绑定事件，事件委托

## inline-block元素什么情况下会出现间隙，如何解决？

## 介绍一下盒模型（标准和怪异模式）

## position几种定位方式及区别

## 列举常见的移动端适配方案

## 有一个 div#wrapper 元素，高、宽度都未知。它其中有一个宽高都为 100px 的 div#box 元素，请你完成 CSS，使得 div#box 在 div#wrapper 内水平、垂直方向居中。
```html
<div id="wrapper">
    <div id="box"></div>
</div>
```
```css
#wrapper{



}

#box {







}
```

## cookie，sessionStorage 和 localStorage 的区别及不同的应用场景

## 实现两栏布局，左边固定宽度，右边自适应。

## 常见的HTTP状态码及含义

## 列举几个熟悉的es6特性

## 假设在 a.com域下有一段js代码需要异步请求b.com域下的数据，会出现什么问题，如何解决？


## 前端性能优化

## js如何实现继承（es5和es6）

## 谈谈vue,react,angular等单页面应用相比以前jquery方式的优缺点