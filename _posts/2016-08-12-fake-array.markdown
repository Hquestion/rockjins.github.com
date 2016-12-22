---
layout:     post
title:      " 如何伪造数组？ "
subtitle:   " Camouflage is the most basic skills of a ninja. "
date:       2016-07-01
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-5cea7011542ce57d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - Array
    - Object
    - Function
    - JavaScript

---

> 真的假不了，假的真不了。

我们经常可以从各种库或框架中拿到这样的值：

明明是一个对象，却有length属性；或者明明看上去是个数组，却不能使用数组的方法（arguments）。我们今天就来聊聊怎么伪造数组。

有时，我们想创建一个包含数组数据的对象，如果仅仅是集合，只要使用数组就行。但很多时候，我们还要保存一些与集合相关的元数据。

我们可以给普通对象添加一些我们想要的功能，让它看起来像一个数组吗？Array的原型链上有很多处理集合的方法，我们可以把这些方法嫁接到自己的对象上吗？

事实证明是可以的：

```javascript
var elems = {

  length: 0,                                                

  add: function(elem){                                      
    Array.prototype.push.call(this, elem);
  },

  gather: function(id){                                     
    this.add(document.getElementById(id));
  }
};

elems.gather("first");                                     

elems.gather("second");              

console.log(elems);                   
```

在这个例子中，我们给elems对象添加了一些模拟数组的行为，首先定义了length属性，用于保存元素个数。

之后定义了一个方法，用于将元素添加到模拟数组的结尾。我们使用了原生数组的方法：`Array.prototype.push`,而不是自己编写代码。

正常情况下，`push`方法是通过其函数上下文操作自身数组的，在这里我们用`call`方法强制用我们自己的对象作为`push`的函数上下文。

`push`函数会增加length属性，并给对象添加一个数字属性，再将其引用到传入的元素上。在某种程度上来说，这是颠覆性的！

`add`方法期望接收一个用于储存的元素引用，所以，我们为了方便，定义了`gather`方法，用于根据id值查找对应元素，并调用`add`方法将其添加到储存中。

我们打印出`elems`对象看一看：

![](https://upload-images.jianshu.io/upload_images/2859850-bd6b647f0354c477.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这就是我们想要的！

当然，这只是表面我们看到的，关于伪造数组，还有很多的知识要了解，这里只是告诉你它的基本实现，有兴趣了解更多的话，Google一下吧！
