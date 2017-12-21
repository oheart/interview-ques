## 知识点
1. 常用日期对象方法
```js
var date = new Date();  //获取一个时间对象  
date.getFullYear();  //年（完整的年份，4位，1970）  
date.getMonth();  //月（0-11，0代表1月，用的时候记得加1）
date.getDate();   //日（1-31）
date.getTime();  // 获取时间(从1970.1.1开始的毫秒数)
date.getHours();  //时（0-23）
date.getMinutes(); //分（0-59）
date.getSeconds(); //秒（0-59）
```
2. 获取时间戳方法
- 时间戳： 指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数。
- 三种方法： parse、valueOf、getTime
```js
var timestamp1 = Date.parse(new Date());
var timestamp2 = (new Date()).valueOf();
var timeStamp3 = new Date().getTime();
```
- 区别：
    - parse： 只能精确到秒，毫秒用0来代替
    - valueOf和getTime会精确到毫秒
## 考题
1. 写一个函数，把时间戳 1513505046 转为日期 2017-12-17 18:04:06 格式
```js
function formateDate(date){
                var date = new Date(date*1000);   //如果date为13位不需要乘1000

                var getYear = date.getFullYear(),
                    getMonth = date.getMonth() + 1,
                    getDate = date.getDate(),
                    getHours = date.getHours(),
                    getMinutes = date.getMinutes(),
                    getSeconds = date.getSeconds()

                var Y = getYear,
                    M = getMonth < 10 ? '0' + getMonth : getMonth,
                    D = getDate < 10 ? '0' + getDate : getDate,
                    h = getHours < 10 ? '0' + getHours : getHours,
                    m = getMinutes < 10 ? '0' + getMinutes : getMinutes,
                    s = getSeconds < 10 ? '0' + getSeconds : getSeconds

                return Y + '-' + M + '-' + D + ' ' + h + ':' + m + ':' + s;
}
          
formateDate(1513505046)
```
## 参考链接
1. <a href="https://segmentfault.com/a/1190000006160703" target="_blank">JavaScript获取时间戳与时间戳转化</a>
2. <a href="https://segmentfault.com/a/1190000000481753" target="_blank">js时间戳与日期格式之间的互转</a>

