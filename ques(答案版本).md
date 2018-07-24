### 1. 介绍一下盒模型（标准和怪异模式）

在标准模式（w3c标准盒模型）下，一个块总宽度（总宽度 = width + margin + padding + border).  
在怪异模式（IE标准盒模型）下， 一个块总宽度 （总宽度= width + margin）—> width包含padding和border. 

避免触发IE盒模型的方法是使用<!DOCTYPE html>声明，告诉IE采用W3C盒子模型即可。

css3中新增了一种盒模型计算方式：border-sizing. 
如果border-sizing：border-box，此时将采用怪异模式解析计算：
	那么布局所占宽度为     
   &nbsp;&nbsp;&nbsp;总宽度 = width（包含padding和border）  
   &nbsp;&nbsp;&nbsp;总高度 = height（包含padding和border）


### 2. position几种定位方式及区别

static(默认), fixed, relative, fixed; 
 
static：默认值，即正常文档流的表现形式，普通流中的元素的位置由元素在 (X)HTML 中的位置决定。  

relative：相对定位，对于其原本位置进行定位，但是其原来所占用的空间依然存在，即不脱离文档流。如”left:20px” 会使元素的left距离原来的位置添加 20 像素。  

absolute：绝对定位，相对于 static 定位以外的第一个父元素进行定位。脱离文档流，不占据空间，元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。

fixed: 绝对定位，脱离所有元素，相对于浏览器窗口进行定位。元素的位置通过 “left”, “top”, “right” 以及 “bottom” 属性进行规定。

### 3. 实现两栏布局，左边固定宽度，右边自适应。

```html
<div id="left">Left sidebar</div>
<div id="content">Main Content</div>
```

第一种： 浮动布局

```CSS
#left { float: left; width: 220px; background-color: green; }  
#content { background-color: orange; margin-left: 220px;
``` 

第二种： 浮动和负边距实现

```css
    #left {
        background-color: green;
        float: left;
        width: 220px;
        margin-right: -100%;
    }

    #content {
        float: left;
        width: 100%;
    }
```

第三种，利用BFC

```css
   #lef{float:left;width: 220px;height: 300px;background: blue;}
   #content{overflow: hidden; background: pink;height: 500px;}
```
第四种， 定位

```css
 #left{position:absolute;top: 0;left: 0; width: 300px;height: 220px;background: blue;}
 #content{margin-left: 220px;background: pink;height: 500px;}
```



4. **实现未知高宽元素垂直居中**

    absolute+margin:auto
    
    ```css
    .parent{
               position:relative;
    }
    .child{
                position:absolute;
                left:0;
                right:0;
                top:0;
                bottom:0;
                margin:auto;
    }
    ```
    transform居中
    
    ```css   
    .parent {
            position: relative;
    }
    .child {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
    }
    ```

    flex居中
    
    ```css 
    .flex-center-justify{
            display:flex;
            justify-content:center; /*水平居中*/
            align-items:center; /*垂直居中*/
    }
    ```      

### 5. 列举常见的移动端适配方案
viewport，rem, vw vh, 百分比, media, flex, grid, box-sizing...

### 6. 以下代码会输出什么？
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



### 7. 以下代码会输出什么？
```js
var a = function(){
    console.log(i);  
    var i = 1;
    console.log(i);    
}
a();
```
```
答案：  undefined， 1   
考点： var声明的变量提升 

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

### 8. 以下代码会输出什么？
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


### 9. 以下会输出什么？如何改进？
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
   
**IIFE立即执行函数** 

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
**let**

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

### 10. **DOM结构为**
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

### 11. 什么是事件流？DOM事件流分为几个阶段？
    答案：     
    事件流：事件流所描述的就是从页面中接受事件的顺序。事件流有两种，分别是事件冒泡和事件捕获。  

    DOM事件流包括三个阶段。  
    事件捕获阶段    
    处于目标阶段    
    事件冒泡阶段    


### 12. cookie，sessionStorage 和 localStorage 的区别及不同的应用场景。

相同点：都是存储数据，存储在web端，并且都是同源

不同点：
（1）cookie 只有4K 小 并且每一次请求都会带上cookie 体验不好，浪费带宽  
（2）session和local直接存储在本地，请求不会携带，并且容量比cookie要大的多  
（3）session 是临时会话，当窗口被关闭的时候就清除掉 ，而 local永久存在，cookie有过期时间  
（4）cookie 和local都可以支持多窗口共享，而session不支持多窗口共享 但是都支持a链接跳转的新窗口

### 13. 假设在 a.com域下有一段js代码需要异步请求b.com域下的数据，会出现什么问题，如何解决？
	会出现跨域问题。  
	- jsonp 前端传递callback参数（?callback=appendHtml），后台把返回数据用callback包裹( appendHtml(["数据1","数据2","数据3"]) )，前端用callback获取数据。
	本质上创建了一个script标签，script可以加载任何东西（js,txt,xhr...）,相当于把请求的东西放在本地然后当做js执行。
	- CORS 利用同源策略，后台处理返回响应头（Response Headers）：Access-Control-Allow-Origin: */指定域名
	- document.domain
	- 使用HTML5的postMessage方法
	- nginx等中间层转发
	- webpackDevServer的proxy


###14. 列举几个熟悉的es6特性
let,const,rest参数，promise, async await, Map和Set....

###15. 前端性能优化
cdn, 雪碧图，懒加载，减少重绘重排， 利用http缓存（304和200 from cache）, 压缩图片...

###16. 获取单独一篇的文章页请求需要依赖于获取文章信息和获取该文章下所有留言这两个接口请求，请用代码实现单独一篇的文章页请求。
    ```js
    // 获取文章信息接口请求
    function getPostById(){}

    //获取该文章下所有留言接口请求
    function getComments(){}

    // 获取单独一篇的文章页请求
    function  getSimpleArticle(){      // 这里需要填写，写出大概即可

        Promise.all([
        getPostById(){}, //获取文章信息
        getComments(){} //获取该文章所有留言
        ])
        .then(function(result){
            var post = result[0];
            var comments = result[1];
            if(!post){
                throw new Error('该文章不存在');
            }
            res.render('post',{
                post: post,
                comments: comments
            })
        })
        .catch(next);
    }
    ```






