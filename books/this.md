## 知识点

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


