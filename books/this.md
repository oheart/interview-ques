## 知识点
1. 三种变量
- 实例变量：（this）类的实例才能访问到的变量

- 静态变量：（属性）直接类型对象能访问到的变量

- 私有变量：（局部变量）当前作用域内有效的变量

举例：
```js
function ClassA(){
    var a = 1; //私有变量，只有函数内部可以访问
    this.b = 2; //实例变量，只有实例可以访问
}

ClassA.c = 3; // 静态变量，也就是属性，类型访问

console.log(a); // error
console.log(ClassA.b) // undefined
console.log(ClassA.c) //3

var classa = new ClassA();
console.log(classa.a);//undefined
console.log(classa.b);// 2
console.log(classa.c);//undefined
```
2. call、apply 、函数执行的本质
当我们执行一个函数，以下几种调用方式等价
```js
"use strict"
function fn(a,b){
    console.log(this)
}
fn(1, 2)

//等价于
fn.call(undefined, 1, 2)
fn.apply(undefined, [1, 2])
```
在严格模式下， fn 里的 this 就是 call 的第一个参数，也就是 undefined。
在非严格模式下(不加"use strict")， call 传递的第一个参数如果是 undefined 或者 null， 那 this 会自动替换为 Window 对象
```js
var obj = {
    fn: function(a, b){
        console.log(this)
    },
    child: {
        fn2: function(){
            console.log(this)
        }
    }
}
obj.fn(1, 2)
//等价于
obj.fn.call(obj, 1, 2)         // 所以 this 是 obj
obj.fn.apply(obj, [1, 2])

obj.child.fn2()
//等价于
obj.child.fn2.call(obj.chid)    // 所以 this 是 obj.child
```
以上就是原理，我们根据原理来发散做几道测试题

```js
let name = '饥人谷'
let people = {
    name: '若愚',
    sayName: function(){
        console.log(this.name)
    }
}
let sayAgain = people.sayName
function sayName(){
    console.log(this.name)
}

sayName()
/*
 解析：相当于 `sayName.call(undefined)` ，因为是非严格模式，所以 this 被替换成 Window，所以这里输出全局的 name 即 "饥人谷"
*/
people.sayName()
/*
解析: 相当于 `people.sayName.call(people)` ，所以这里输出 `people.name` 即 "若愚"
*/

sayAgain()
/*
解析: 相当于 `sayAgain.call(undefined)` ，，因为是非严格模式，所以 this 被替换成 Window，所以这里输出全局的 name 即 "饥人谷"
*/

```
```js
var arr = []
for(var i=0; i<3; i++){
    arr[i] = function(){ console.log(this) }
}
var fn = arr[0]

arr[0]
/*
解析: 因为函数是个特殊的对象，所以 arr 相当于 { '0': function(){}, '1': function(){}, '2': function(){}, length:3}
arr[0]相当于 `arr['0']` 相当于 `arr.0` （当然这种写法不符合规范），所以 arr[0]等价于 arr.0.call(arr), this就是 arr
*/

fn()
/*
解析: 相当于 `fn.call(undefined)`， 所以 fn 里面的 this 是 Window
*/
```
3. bind
bind 的作用和 call 与 apply 类似，区别在于使用上
bind 的执行的结果返回的是绑定了一个对象的新函数
```js
var obj = {name: '饥人谷'}
function sayName(){
    console.log(this.name)
}
var fn = sayName.bind(obj)  // 注意 这里 fn 还是一个函数，功能和 sayName 一模一样，区别只在于它里面的 this 是 obj
fn() // 输出： '饥人谷' 
```
一个实际点的例子
```js
var app = {
    container: document.querySelector('body'),
    bind: function(){
        this.container.addEventListener('click', this.sayHello)                  //点击的时候会执行 sayHello，sayHello 里面的 this 代表 body 对象
        this.container.addEventListener('click', this.sayHello.bind(this))  //点击的时候会执行 sayHello，sayHello 里面的 this 代表 app 对象
    },
    sayHello: function(){
       console.log(this)
    }
}
app.bind()
```
4. 箭头函数

如果你经常用 ES6语法，你会发现关于函数这两种写法
```js
let app = {
    fn1: function(a){
        console.log(this)  //app
    },
    fn2(a) {
        console.log(this)  //app
    },
    fn3: (a)=>{
        console.log(this)  //window
    }
}

// 粗略一看，fn1、fn2、fn3 貌似都一样，实际上 fn1和 fn2完全等价，但 fn3是有区别的
// 以上代码等同于

app.fn2.call(app)
app.fn3.call( 它的上一级的 this )
```

## 考题
```js
var name = 'outername';
var object = {
    name: 'innername',
    sayName: function(){
            return this.name;
    }
}
object.sayName();  //innername
```

```js 
  function a(){
            console.log(this);
  }
  a.call(null);  //window
```

```js
function Foo(){
           this.id = 'foo instance'
}    
Foo.id = 'foo';
Foo.prototype.sayName = function(){
    console.log(this.id)
}
Foo.sayName = function(){
    console.log(this.id)  
}

Foo.sayName();   //foo 
new Foo().sayName();   //foo instance
var func = Foo.sayName;
func();  //undefined
```

```js
var obj = {
    a: 1,
    getA: function(){
        var a = 2;
        setTimeout(function(){
            console.log(this.a);
        },1000)
    }
}
obj.getA();   //undefined

// 以上代码相当于

var obj = {
    a: 1,
    getA: function(){
        var a = 2;
        function fn(){
            console.log(this.a);
        }
        //过10ms 后执行
        //fn.call(undefined) ，所以this指向Window,全局环境下找不到变量a,故输出undefined
    }
}
obj.getA();   //undefined
```


```js
var app = {
    fn1() {
        setTimeout(function(){
            console.log(this)
        }, 10)
    },
    fn2() {
        setTimeout(()=>{
            console.log(this)
        },20)
    },
    fn3() {
        setTimeout((function(){
            console.log(this)
        }).bind(this), 30)        
    },
    fn4: ()=> {
        setTimeout(()=>{
            console.log(this)
        },40)        
    }
}
app.fn1()
app.fn2()
app.fn3()
app.fn4()

// 以上代码相当于
var app = {
    fn1() {
        function fn(){
            console.log(this)
        }
        //过10ms 后执行
        //fn.call(undefined) ，所以输出 Window
    },
    fn2() {
        //过20ms 执行箭头函数
        //箭头函数里面没资格有 自己的 this，借用 setTimeout 外面的 this，也就是 app
    },
    fn3() {
        // 创建了一个新函数，这个新函数里面绑定了 外面的this，也就是 app
        // 20 ms 后执行新函数，输出 this，也就是刚刚绑定的 app    
    }
    fn4: ()=> {
        //过40ms 执行箭头函数
        //箭头函数里面没资格有 this，用 setTimeout 外面的 this
        //setTimeout 所在的 fn4也是箭头函数，没资格拥有自己的 this，借用外面的 this ，也就是 Window     
    }
}
```

## 参考链接
1. <a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this" target="_blank">this</a>
2. <a href="https://xiedaimala.com/courses/b8b4c00c-6798-4caf-8bfe-ba9fbb4c6d3d/tasks/ffbb7825-1793-4793-9477-ee5a34614210" target="_blank">你不知道的 this</a>
3. <a href="http://book.jirengu.com/fe/%E5%89%8D%E7%AB%AF%E8%BF%9B%E9%98%B6/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1/this.html" target="_blank">What's this?</a>
4. <a href="https://www.cnblogs.com/coco1s/p/4833199.html" target="_blank">深入浅出 妙用Javascript中apply、call、bind</a>
5. <a href="http://www.jianshu.com/p/56a9c2d11adc" target="_blank">深入浅出 妙用Javascript中apply、call、bind</a>
6. <a href="https://zhuanlan.zhihu.com/p/23804247" target="_blank">this 的值到底是什么？</a>
7. <a href="http://blog.jirengu.com/?p=480" target="_blank">你怎么还没搞懂 this？</a>




