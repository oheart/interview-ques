1. 介绍一下盒模型（标准和怪异模式）



2. position几种定位方式及区别



3. 实现两栏布局，左边固定宽度，右边自适应。



4. 有一个 div#wrapper 元素，高、宽度都未知。它其中有一个宽高都为 100px 的 div#box 元素，请你完成 CSS，使得 div#box 在 div#wrapper 内水平、垂直方向居中。
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
5. 列举常见的移动端适配方案

6. 以下代码会输出什么？
```js
var a = 10;
var b = a;
a++;
console.log(a); 
console.log(b); 
```
答案： 11， 10  
考点： 基本类型的比较是值的比较。基本类型的值一经确定就不可改变，基本类型的值的赋值是简单赋值如果从一个变量向另一个变量赋值基本类型的值，会在变量对象上创建一个新值，然后把改值复制到为新变量分配的位置上。  
上面代码中，a中保存的是10.当使用a的值来初始化b时，b中也保存了值10.但b中的10和a中的10是完全独立的。b中的值只是a中值的一个副本，所以这两个变量可以参与任何操作而不会相互影响。



```js
var person1 = {};
var person2 = {};
console.log(person1 == person2);
```
答案： false  
考点： 引用类型的比较是引用的比较。引用类型是按引用访问的，换句话说就是比较两个对象的堆内存中的地址是否相同，person1和person2指向不同的引用，在堆内存中地址是不同的，这两个是完全不同的对象，所以返回false。



7. 以下代码会输出什么？
```js
var a = function(){
    console.log(i);  
    var i = 1;
    console.log(i);    
}
a();
```
输出：

```js
var a = function(){
    console.log(i);
    let i = 1;
    console.log(i);
}
a();
```
输出：

```js
let i = 2;
var a = function(){
    console.log(i);
    let i = 1;
}
a();
```
输出：

8. 以下代码会输出什么？
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
输出：


9. 以下会输出什么？如何改进？
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
输出：

10. DOM结构为
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

11. 什么是事件流？DOM事件流分为几个阶段？  
答案：     
事件流： 事件流所描述的就是从页面中接受事件的顺序。事件流有两种，分别是事件冒泡和事件捕获。  

DOM事件流包括三个阶段。  
事件捕获阶段    
处于目标阶段    
事件冒泡阶段    


12. cookie，sessionStorage 和 localStorage 的区别及不同的应用场景。


13. 假设在 a.com域下有一段js代码需要异步请求b.com域下的数据，会出现什么问题，如何解决？
会出现跨域问题。  
- jsonp 前端传递callback参数（?callback=appendHtml），后台把返回数据用callback包裹( appendHtml(["数据1","数据2","数据3"]) )，前端用callback获取数据。
本质上创建了一个script标签，script可以加载任何东西（js,txt,xhr...）,相当于把请求的东西放在本地然后当做js执行。
- CORS 利用同源策略，后台处理返回响应头（Response Headers）：Access-Control-Allow-Origin: */指定域名
- document.domain
- 使用HTML5的postMessage方法
- nginx等中间层转发
- webpackDevServer的proxy


14. 列举几个熟悉的es6特性

15. 前端性能优化

16. 谈谈vue,react,angular等单页面应用相比以前jquery方式的优缺点






