---
layout:     post
title:      " 使用内联函数进行递归 "
subtitle:   " Recursion is one of the hardest things to understand in the world. "
date:       2016-12-19
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-46bfbe3d67c7aa38.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - JavaScript
    - Function

---

>  我曾经以为匿名函数就是匿名函数，事实上，匿名函数就是匿名函数。

在JavaScript中实现递归有很多种方法，常见的有使用函数名调用自身、使用arguments.callee。

现在有这么一个例子，判断一个字符串是不是回文，返回'true'或'false'。

我们把递归函数赋值给一个对象的属性：

```javascript
var JudgeTool = {
  isPalindrome : function (text){
    if (text.length <= 1) return true;
    if (text.charAt(0) != text.charAt(text.length - 1)) return false;
    return Judge.isPalindrome(text.subString(1,text.length - 2));
  }
}
```

我们可以用一个回文字符串测试一下：

```javascript
JudgeTool.isPalindrome("htmlmth"); //返回true
```

功能是实现了，但是，如果另一个对象也想拥有一个同样功能的方法，我们或许可以这样做：

```javascript
var AnotherTool = {
  isPalindrome:JudgeTool.isPalindrome
}
```

没有问题，我们依然可以用`AnotherTool.isPalindrome`方法去判断字符串是否是回文，但是，如果我在`AnotherTool`对象后面加一句：

```javascript
JudgeTool = {};
```

大家可以想到，肯定会出错，因为在递归函数内部调用的是`Judge.isPalindrome()`，现在Judge对象被重置，那肯定取不到这个对象的属性了。

那我们改写一下函数内部的递归调用：

```javascript
var JudgeTool = {
  isPalindrome : function (text){
    if (text.length <= 1) return true;
    if (text.charAt(0) != text.charAt(text.length - 1)) return false;
    return this.isPalindrome(text.subString(1,text.length - 2));
  }
}
```

我们只改写了一处，把`Judge.isPalindrome`改成了`this.isPalindrome`，现在再清空`Judge`对象，我们还是能够调用`AnotherTool.isPalindrome`，因为this是指向当前调用此方法的对象。

但问题又来了，我们的方法名必须为：`isPalindrome`，如果我不想叫这个方法名，又或者函数的其中一个引入不是对象的属性怎么办？这时候就要引入内联函数的概念了。

看下例子，我们可以这样改写Judge对象：

```javascript
var JudgeTool = {
  isPalindrome : function same(text){
    if (text.length <= 1) return true;
    if (text.charAt(0) != text.charAt(text.length - 1)) return false;
    return same(text.subString(1,text.length - 2));
  }
}
```

注意，我们只给匿名函数加了一个名字，并且在内部用这个名字去调用它，这样，不管外面的方法名怎么变，都不会影响到内部的函数运行。

这个技巧在很多地方都有用到，如果你有看jQuery源码的话。

而且有趣的是，在函数内部，`JudgeTool.isPalindrome == same` 为`true` 。

尽管我们可以给内联函数进行命名，但这个名称只在函数内部可见，你可以把内联函数的名称想象成函数内的一个变量，它的作用域仅限于函数的内部。

我们看这样一个例子就明白了：

```javascript
var foo = function bar(){
  typeof bar;//返回function
}

typeof bar;//返回undefined
```

这个技巧在递归中常常会用到，如果你留意的话。

> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
