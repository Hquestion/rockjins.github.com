---
layout:     post
title:      " 带你切身体验实例被new出来的过程 "
subtitle:   " True feelings. "
date:       2017-01-18
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-dd0abd9afc1ec5bc.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - JavaScript
    - Object

---

>  其实费尽心力探寻底层实现就是为了用来装逼 😝

### 闲话

网上有很多帖子、文章介绍new操作符运行步骤的文章，但我感觉读者看完之后还是会很模糊，知其然，不知其所以然。

好，轮到我装逼了！

首先，读这篇文章，你得对原型链和构造函数有个基本的认识，否则收益不会很大，反而会更懵逼。

### 正文

我们先创建一个简单的构造函数：

```javascript
function Rocker(name){
  this.name = name;
};

Rocker.prototype.getName = function(){
  return this.name;
}
```

这是最简单不过的构造函数了，正常情况下，我们要生成他的一个实例，只需要：

`var someOne = new Rocker('Max')`

这样就实例化了一个对象，但是，实例化的过程是怎样的呢？

可能很多朋友在网上也看了很多文章，new的过程不就是三步吗？

> 1. 开辟一个块内存，创建一个空对象
>
> 2. 执行构造函数，对这个空对象进行构造
>
> 3. 给这个空对象添加__proto__属性

没错，是这三步，但是你真的理解了吗？至少我第一次看挺懵逼的。

好吧，最直观的方法就是，把创建一个对象的过程用代码体现出来，这样才能装逼嘛...

#### 体验

让我们创建一个函数，来实现上面new操作符的功能：

```javascript
var createObject = function(){
  var obj = new Object(),   //(1)
      Constructor = [].shift.call(arguments);   //(2)

  obj.__proto__ = Constructor.prototype;    //(3)

  var ret = Constructor.apply(obj, arguments);    //(4)

  return typeof ret === 'object' ? ret : obj;   //(5)
};

var shock = createObject(Rocker, 'Shock');

console.log(shock.name);  //Shock

console.log(shock.getName());  //Shock

console.log(Object.getPrototypeOf(shock) === Rocker.prototype); //true
```

就是上面这几句代码，向你展现了一个实例被new出来的过程。

#### 分析一下

我们来简单分析一下吧，其实很清晰明了了。

在`(1)`处，我们创建了一个空对象（准确的说是克隆了Object.prototype对象）

接下来`(2)`取到构造函数，赋值给Constructor变量，也就是说Rocker构造函数变成Constructor的一个引用了

接着`(3)`把Constructor.prototype（也就是Rocker.prototype）赋值给(1)刚刚创建的obj的原型链，或者这么说，把obj的原型链指向Constructor的原型

`(4)`我们用apply改变this的指向，用obj代替Constructor构造函数内部的this，并把arguments作为参数传入（在第2步时已经用shift把第一个参数去除了），此时的ret已经是一个合格的实例了！

保险起见，我们`(5)`返回时判断ret是否是对象，如果不是就返回一个空对象（因为很多人真的不会按照规矩传参！！！）

这时候我们再外部调用这个函数试试，实时证明确实能达到new的效果。

再用getPrototypeOf方法测试一下，shock的原型链真的指向Rocker的原型！

这就是实例被new出来的过程，你明了吗？

其实上面代码有很多小技巧，可以细细咀嚼。

> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
