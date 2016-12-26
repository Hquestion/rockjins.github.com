---
layout:     post
title:      " 由Vue引发的getter和setter思考 "
subtitle:   " Thinking can make you stronger. "
date:       2016-10-25
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-6142a6b04f7319fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - Vue
    - JavaScript

---

> 接触新事物总会让人很难受，但也会让人成长。

公司的新项目决定使用Vue.js来做，当我打印出Vue实例下的data对象里的属性时，发现了一个有趣的事情：

![](http://images2015.cnblogs.com/blog/929120/201610/929120-20161025151218546-1679290074.png)

它的每个属性都有两个相对应的get和set方法，我觉的这是多此一举的，于是去网上查了查Vue双向绑定的实现原理，才发现它和Angular.js双向绑定的实现原理完全不同，Angular是用的数据脏检测，当Model发生变化，会检测所有视图是否绑定了相关数据，再更改视图。而Vue使用的发布订阅模式，是点对点的绑定数据。

Vue的数据绑定只有两个步骤，compile=>link。

我一直在想，vue是通过什么去监听用户对Model的修改，直到我发现Vue的data里，每个属性都有set和get属性，我才明白过来。

在平时，我们创建一个对象，并修改它的属性，是这样的：

```javascript
var obj = {
  val:99
}
obj.val = 100;
console.log(obj.val)//100
```

没有任何问题，但是如果要你去监测，当我修改了这个对象的属性时，要去做一些事，你会怎么做？

这就要用到getter和setter了。

假设我现在要给一个码农对象添加一个name属性，而且每次更新name属性时，我要去完成一些事，我们可以这样做：

```javascript
var Coder = function() {
        var that = this;
        return {
            get name(){
                if(that.name){
                    return that.name
                }
                return '你还没有取名'
            },
            set name(val){
                console.log('你把名字修成了'+val)
                that.name = val
            }
        }
    }
    var isMe = new Coder()
    console.log(isMe.name)
    isMe.name = '周神'
    console.log(isMe.name)
    console.log(isMe)
```

输出：

![](http://images2015.cnblogs.com/blog/929120/201610/929120-20161025173135343-1508869676.png)

你会发现这个对象和最上面的Vue中的data对象，打印出来的效果是一样的，都拥有get和set属性。

我们来一步步分析下上面的代码,很有趣。

我们先创建一个对象字面量：

var Coder = function() {...}

再把this缓存一下：

var that = this;

接下来是最重要的，我们return了一个对象回去：

```javascript
{
  get name(){/*do something*/},

  set name(val){/*do something*/}
}
```

顾名思义，get为取值，set为赋值，正常情况下，我们取值和赋值是用obj.prop的方式，但是这样做有一个问题，我如何知道对象的值改变了？所以就轮到set登场了。

你可以把get和set理解为function，当然，只是可以这么理解，这是完全不一样的两个东西。

接下来创建一个码农的实例，isMe；此时，isMe是没有name属性的，当我们调用isMe.name时，我们会进入到get name(){...}中，先判断isMe是否有name属性，答案是否定的，那麽就添加一个name属性，并给它赋值："你还没有取名"；如果有name属性，那就返回name属性。

看到这里你一定知道get怎么使用了，对，你可以把get看成一个取值的函数，函数的返回值就是它拿到的值。

我感觉比较重要的是set属性，当我给实例赋值：

isMe.name="周神"

此时，会进入set name(val){...}；形参val就是我赋给name属性的值，在这个函数里，我就可以做很多事了，比如双向绑定！因为这个值的每次改变都必须经过set，其他方式是改变不了它的，相当于一个万能的监听器。

还有另一种方法可以实现这个功能。

ES5的对象原型有两个新的属性__defineGetter__和__defineSetter__，专门用来给对象绑定get和set。可以这样书写：

```javascript
var Coder = function() {
    }
    Coder.prototype.__defineGetter__('name', function() {
        if (this.name) {
            return this.name
        }else{
            return '你还没有取名'
        }
    })
    Coder.prototype.__defineSetter__('name', function(val) {
        this.name = val
    })
    var isMe = new Coder()
    console.log(isMe.name)
    isMe.name = '周神'
    console.log(isMe.name)
    console.log(isMe)
```

效果是一样的，建议使用下面这种方式，因为是在原型上书写，所以可以继承和重用，最近想写点小框架，才发现知识不够用，大家一起加油吧！

本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
