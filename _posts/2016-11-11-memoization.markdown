---
layout:     post
title:      " 使用自记忆函数提高页面性能 "
subtitle:   " Everything has its dialectical nature. "
date:       2016-11-11
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-c4cf4afa0a1cfd80.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - Function
    - JavaScript

---
> 当你真正想要提高页面性能，你会发现你的代码和屎没两样。

自记忆函数这个名字听起来有点奇怪，这只是人们给它取的一个名字罢了。

在JavaScript中，函数是第一型对象，所以它可以拥有自己的属性，我们就可以利用这一点来进行数据的缓存。

还是先看一个例子，`isPrime`函数用来判断参数是否是素数，和普通函数唯一的不同在于我们暗中创建了一个`answers`缓存：

```javascript
function isPrime(value) {
  if (!isPrime.answers) isPrime.answers = {};                  
  if (isPrime.answers[value] != null) {                        
    return isPrime.answers[value];                             
  }                                                            
  var prime = value != 1; // 1永远都不会是素数
  for (var i = 2; i < value; i++) {
    if (value % i == 0) {
      prime = false;
      break;
    }
  }
  return isPrime.answers[value] = prime;                       
}

isPrime(5)//true                            
isPrime.answers[5]//true
```

我们首先判断`isPrime`函数是否有`answers`属性，没有就创建一个。

接下来我们检查`answers`是否存在参数值对应的结果，在该缓存里，我们用参数值作为属性的`key`，如果发现缓存结果，则直接返回它。

如果在缓存中没有找到结果，就计算该参数判断是不是素数。

最后返回判断结果，并赋值给`answers`属性的`[value]`。

下面的测试证明，确实可以从`isPrime.answers`中取到之前计算过的结果。

当有大量数据需要计算，并且数值很大的情况下，这种性能的优化可能会大到你无法想象。

在我们实际工作中可能很少去计算素数，那再举一个大家常见的例子，缓存DOM元素。

通过标签查询DOM元素是我们常常做的一件事，但频繁操作性能很糟糕，我们可以利用刚刚学会的缓存记忆创建一个缓存，保存已匹配到的元素集合：

```javascript
function getElements(name){
  if (!getElements.cache) getElements.cache = {};
  return getElements.cache[name] =
    getElements.cache[name]||
    document.getElementsByTagName(name);
}
```

其实缓存代码非常简单，并不会给你的代码逻辑增加太多复杂性，但是，上面这几行简单的缓存代码，就产生了5倍的性能提升，如表：

*所有测试都在chrome53下进行了100000次迭代的毫秒数*

| 代码版本|平均时间|最小时间|最大时间|运行次数|
|:--:|:--:|:--:|:--:|:--:|
|非缓存版本|16.7|18|19|10|
|缓存版本|3.2|3|4|10|

使用自记忆函数技巧，不仅在代码组织上有好处，而且储存对象无需污染作用域，就可以获得性能提升。

缓存记忆有两个主要优点：

- 最终用户享有绝对性能优势。
- 发生在幕后，完全无缝，最终用户和开发人员都无需任何特殊操作或为此做任何额外的初始化做工。

相比优点，也要权衡一下缺点：

- 为提高性能，任何类型的缓存都会牺牲掉内存。

- 纯粹主义认为，储存不应该和业务逻辑放在一起，函数或方法只做一件事，并把它做好。

- 很难进行算法性能的测试

至于，是否运用这种技巧在你项目中，那得看你的实际情况了。

本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
