---
layout:     post
title:      " 不定期更新 JavaScript技巧 "
subtitle:   " Efficiency, is useful. "
date:       2017-01-05
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-13d53baf09a3de93.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - JavaScript

---

>  JavaScript技巧，偶尔更新。

### 计算数组的极值

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

### 迭代arguments

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

### 使用IIFE解决循环问题

*unexpected:*

```javascript
var funcs = [];

for (var i = 0; i < 10; i++) {
    funcs.push(function() { console.log(i); });
}

funcs.forEach(function(func) {
    func();     // 输出数值 "10" 十次
});
```

*expected:*

```javascript
var funcs = [];

for (var i = 0; i < 10; i++) {
    funcs.push((function(value) {
        return function() {
            console.log(value);
        }
    }(i)));
}

funcs.forEach(function(func) {
    func();     // 从 0 到 9 依次输出
});
```

### 使用let解决循环问题

这是`let`独有的特性([参考](https://sagittarius-rev.gitbooks.io/understanding-ecmascript-6-zh-ver/content/chapter_1.html#let-declarations-in-loops))
```javascript
var funcs = [];

for (let i = 0; i < 10; i++) {
    funcs.push(function() {
        console.log(i);
    });
}

funcs.forEach(function(func) {
    func();     // 从 0 到 9 依次输出
})
```

### 判断两个小数是否相等

```javascript
//因为javascript数字通常被输入为十进制的浮点数，但内部却被表示为二进制，所以计算结果会有偏差：

0.1 + 0.2 //0.30000000000000004

0.1 + 1 - 1 //0.10000000000000009

0.1 + 0.2 === 0.3 //false

//所以我们不应该直接比较非整数，而是取其上限，把误差计算进去
//这样一个上限称为 machine epsilon，双精度的标准epsilon值是2^-53

const EPSILON = Math.pow(2, -53); //1.1102230246251565e-16

function epsEqu(x,y) {
  return Math.abs(x - y) < EPSILON;
}

epsEqu(0.1+0.2, 0.3) //true
```



> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
