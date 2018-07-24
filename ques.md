1. **介绍一下盒模型（标准和怪异模式）**





2. **position几种定位方式及区别**






3. **实现两栏布局，左边固定宽度，右边自适应。**
    ```html
    <div id="left">Left sidebar</div>
    <div id="content">Main Content</div>
    ```
    ```css
    #left { 
        
    }
    #content { 

    }
    ```




4. **实现未知高宽元素垂直居中**

5. **列举常见的移动端适配方案**




6. **以下代码会输出什么？**
    ```js
    var a = 10; 
    var b = a;
    a++;
    console.log(a); 
    console.log(b); 
    ```
    输出： 


    ```js
    var person1 = {};
    var person2 = {};
    console.log(person1 == person2);
    ```
    输出： 


7. **以下代码会输出什么？**
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

8. **以下代码会输出什么？**
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


9. **以下会输出什么？如何改进？**
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

10. **DOM结构为**
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

11. **什么是事件流？DOM事件流分为几个阶段？**

12. **cookie，sessionStorage 和 localStorage 的区别及不同的应用场景。**


13. **假设在 a.com域下有一段js代码需要异步请求b.com域下的数据，会出现什么问题，如何解决？**


14. **列举几个熟悉的es6特性**


15. **谈谈你对前端性能优化的理解(可从不同角度出发)**


16. **获取单独一篇的文章页请求需要依赖于获取文章信息和获取该文章下所有留言这两个接口请求，请用代码实现单独一篇的文章页请求。**
```js
    // 获取文章信息接口请求
    function getPostById(){}

    //获取该文章下所有留言接口请求
    function getComments(){}

    // 获取单独一篇的文章页请求
    function  getSimpleArticle(){      // 这里需要填写，写出大概即可




    }
```










