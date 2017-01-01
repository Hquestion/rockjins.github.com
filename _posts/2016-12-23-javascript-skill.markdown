---
layout:     post
title:      " 不定期更新 JavaScript技巧 "
subtitle:   " Efficiency, is useful. "
date:       2016-12-29
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-13d53baf09a3de93.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - JavaScript

---

>  JavaScript技巧，偶尔更新。

### 计算数组的极值：

```javascript
function smallest(array){                         
  return Math.min.apply(Math, array);             
}                                                 

function largest(array){                          
  return Math.max.apply(Math, array);             
}  

smallest([0, 1, 2.2, 3.3]); // 0

largest([0, 1, 2.2, 3.3]); // 3.3
```

### 迭代arguments：

```javascript
function useCall() {
    [].forEach.call(arguments, function(val, key) {
        console.log(key, val)
    });
}

useCall('Bob Dylan', 'Bob Marley', 'Steve Vai');

//0 "Bob Dylan"
//1 "Bob Marley"
//2 "Steve Vai"
```

### Array.prototype.forEach()第二个参数

> [参考：MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)

```javascript
var coder = {
  name: 'Shock',
  friends: ['Rocky', 'Bob'],
  logHiToFriends:function(){
    'use static'
    this.friends.forEach(function(friend){
      console.log(this.name+ ' say hi to '+ friend);
    },this)//注意这个this，如果不添加这个参数，你可以猜测会发生什么
  }
}
```
> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
