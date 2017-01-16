---
layout:     post
title:      " 几分钟帮你理解对象的基本特性之一：多态 "
subtitle:   " Polymorphism is poly + morph + ism. "
date:       2017-01-16
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-68189b93a2e0f6a7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - JavaScript
    - Object
    - Polymorphism
---

>  多态不是简单两句话可以讲清楚，但至少能让你明白它是什么。

### 简单解释多态

拆分一下多态的英文：Polymorphism 就是 poly(复数) + morph(形态) + ism，也就是多种形态。

在JavaScript中，我们可以这样去理解多态：同一操作作用在不同的对象上，可以产生不同的解释和不同的执行结果。

更简单一些说：给不同对象发送同一消息，可能会得到不同的反馈。

### 举个🌰栗子

*Shock是一位吉他手，Alex是一名主唱，当他们听到鼓点响起时，Shock会开始弹吉他，Alex会开始演唱。*

*同样一个鼓点，但Shock和Alex做的事是不同的。*

### 代码实践

下面几行代码简单的把上面的例子实现，说明了对象的多态特性：

```javascript
var playDrum = function(bandsman){
  if(bandsman instanceof Guitarist){
    console.log('哆啦咪嗦啦');
  }else if(bandsman instanceof Singer){
    console.log('We will rock u!')
  }
}

var Guitarist = function(){};

var Singer = function(){};

playDrum(new Guitarist());//哆啦咪嗦啦

playDrum(new Singer());//We will rock u!
```

上面代码虽然实现了"多态"的特性，但这种"多态"是不让人满意的，如果贝斯手来了，我们还得去修改`playDrum`的代码，要知道，修改代码风险太大了，BUG往往就是那个时候出现的。

其实多态背后的核心思想是：将“做什么”和“谁去做以及怎样做”相分离，也就是将“不变的事物”和“可能改变的事物”相分离。

在上面这个例子中，鼓手打鼓是不会改变的，改变的是不同乐手的演奏方式，我们可以将不变的分离出来，把可变的封装起来。

这样我们的代码就是可扩展的，也符合`开放-封闭原则`，这显得优雅和安全的多。

### 升级版🌰栗子

```javascript
var playDrun(bandsman){
  bandsman.play();
}

var Guitarist = function(){};

Guitarist.prototype.play = function(){
  console.log('哆啦咪嗦啦');
}

var Singer = function(){};

Singer.prototype.play = function(){
  console.log('We will rock u!')
}

playDrum(new Guitarist());//哆啦咪嗦啦

playDrum(new Singer());//We will rock u!

```

现在，当吉他手和主唱听到鼓点，他们还是会做出不同的反应。

这时如果贝斯手来了，那很简单，加上贝斯手就行了：

```javascript

var BassPlayer = function(){};

BassPlayer.prototype.play = function(){
  console.log('嗡嗡嗡');//真的不是在黑贝斯...
}

playDrum(new BassPlayer());//嗡嗡嗡
```

以上只是最直观的多态理解方式，还有利用继承得到多态效果、如何利用多态特性进行面向对象编程、多态与设计模式等等。

希望这篇文章能帮到你更好的理解JavaScript中的多态特性。

> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
