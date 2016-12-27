---
layout:     post
title:      " 教你把百度的关键字搜索偷过来用用 "
subtitle:   " Stealing is a kind of virtue, right? "
date:       2016-07-01
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-fb3408173cb6cdd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - JSONP
    - JavaScript

---

> 你真以为我偷东西啊！对啊，我就是偷东西。

话不多说，先上效果图。

![](http://images2015.cnblogs.com/blog/929120/201607/929120-20160701151650890-1741841284.gif)

怎么样，是不是和在用百度一下时，关键字搜索补全一样一样的。

今天下午没什么事，打开百度首页的Newwork看了一下，发现我每次输入内容后，它都会把我们输入的内容发送到后台，后台返回这些关键字的联想条目，我们只需要把这些条目放到页面中，就可以实现上图所示的demo了。

下面我们就来看看怎么获取这些内容。

先打开百度首页，我是用的chrome浏览器，F12，选到Network（你可能发现Network中是空的，刷新一下页面就好了）：

![](http://images2015.cnblogs.com/blog/929120/201607/929120-20160701154248640-1892689881.png)

看到一大堆请求过来的文件，下面我们要找到关键的文件，也就是我们输入时，百度返回的文件，最快速的方法就是输入一大堆的字母，这样可以很方便的找到,我输入了一大堆的ssssss.....：

![](http://images2015.cnblogs.com/blog/929120/201607/929120-20160701154606359-1163344681.png)

看到这些返回的文件吗，wd=ssssssssssss....，我们随便双击一条，把弹出窗口中的Request URL里的网址复制下来，这个就是我们完成关键字搜索的请求路径。

我们可以把网址直接复制到浏览器地址栏，看看得到的是个什么东西:

``` javascript
jQuery110204129574971066774_1467359127325({
"q": "哈哈是什么yisi",
"p": true,
"bs": "",
"csor": "9",
"g": [
{
"q": "哈哈是什么意思",
"t": "n",
"st": {
"q": "哈哈是什么意思",
"new": 0
}
},
{
"q": "哈哈哈哈是什么意思",
"t": "n",
"st": {
"q": "哈哈哈哈是什么意思",
"new": 0
}
}
],
"s": [
"哈哈是什么意思",
"哈哈哈哈是什么意思"
]
});
```

得到的数据是一个对象，不过对象被包裹在一个函数内，这个格式是不是很熟悉啊，对，就是jsonp！分析完这个数据格式，发现我们需要的是这个对象下的s数组里的数据，那我们就把s里的数据拿出来插入到页面中就行了，开始吧！

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
        <script type="text/javascript" src="js/jquery-2.1.0.js" ></script>
    </head>
    <body>
        <input type="text" onkeyup="require()" id="search"/>
        <div id="show"></div>
                <script>
                        //do something......
                </script>
    </body>
</html>
```

这段html代码很简单，引入了jQuery，一个输入框，一个承载返回内容的div，我么直接把script写在body的最下面，当我么输入时手指抬起，就去调用require函数，这个函数里就是我们的关键代码。（大家可以想想为什么要用onkeyup，这是个坑）

```javascript
function require(){
    var search = $("#search").val();
    var _url = 'https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd='+search+'&json=1&p=3&sid=20144_1467_19033_20515_18240_17949_20388_20456_18133_17001_15202_11615&req=2&csor=2&pwd=s&cb=jQuery110207612423721154653_1467355506619&_=1467355506623';
    $.ajax({
        type:"get",
        url:_url,
        async:true,
        dataType:'jsonp',
        jsonpCallback:'jQuery110207612423721154653_1467355506619',
        success:function(data){
            console.log(data);
            var list = data.s;
            var str ="";
            for(var i in list){
                str+='<p>'+list[i]+'</p>';
            }
            $("#show").html(str);
        }
    });
}
```

当require函数被触发时，执行以上代码，我们来分析一下上面的代码。

先获取到输入框的内容，再定义一个_url，把我们之前得到的url地址附给这个变量，但是注意要把关键字的值改成输入框内的值，这样才能动态获取，不然你一直都在请求一个固定的关键字（上面把_url中的search标红加粗了）。

准备工作做好，可以发起ajax请求了，因为是jsonp的格式，所以要设置dataType:'jsonp'，并告诉jQuery回调函数的名称，这个名称可以在浏览器中得到（之前在浏览器地址栏输入url，得到的数据被包含在一个函数里，这里的jsonpCallback就写那个函数的名称，每个人的都不一样）。

现在我们只需要把数据console.log出来，并解析到页面上，就可以实现文章开头的效果了，简单吧！(记得放在服务器环境运行哦！)

> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
