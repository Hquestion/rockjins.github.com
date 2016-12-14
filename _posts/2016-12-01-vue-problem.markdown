---
layout:     post
title:      " Vue数据绑定隐藏的神坑.... "
subtitle:   " Someone walk, will have a road. "
date:       2016-12-01
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-869affe7daaa25d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - Vue
    - JavaScript

---

> 出现问题是好的，那说明你在行动。

今天被Vue的一个坑给折磨了一天，终于发现是什么问题，我们先来模拟一个场景：
代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>vue</title>
</head>
<body>
    <div id="app">
        <input type="text" v-model='sendJson.name'>
        <button @click='showName'>打印输入框的值</button>
    </div>
    <script type="text/javascript" src='./vue.min.js'></script>
    <script type="text/javascript">
    new Vue({
        el:'#app',
        data(){
            return{
                sendJson:{}
            }
        },
        methods:{
            showName(){
                console.log(this.sendJson.name)
            }
        }
    });
    </script>
</body>
</html>
```

我们进页面就点按钮，你猜会输出什么？

是undefined，不算奇怪，你什么都没输入，当然是undefined了。

![](http://images2015.cnblogs.com/blog/929120/201612/929120-20161201171421084-1001813606.png)

OK，接下来刷新页面，进去多一步操作，先点击一下input输入框，在点击按钮，只是多做这一步操作：

![](http://images2015.cnblogs.com/blog/929120/201612/929120-20161201171437131-570191932.png)

输出的是空白，在chrome中空白就代表空字符串，可以修改一下打印结果：

`console.log(this.sendJson.name === "")`

![](http://images2015.cnblogs.com/blog/929120/201612/929120-20161201171456443-1782238340.png)

其实这看起来不是个大问题，但是在我的场景里问题就大了。

我要把输入框内的值作为一个对象的属性，问题就来了，看图：

![](http://images2015.cnblogs.com/blog/929120/201612/929120-20161201171507646-1556743229.png)

这个坑牛逼不，我真是个奇葩。
