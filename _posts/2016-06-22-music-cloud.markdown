---
layout:     post
title:      " 来自网易云的黑科技，带尖角的div...... "
subtitle:   " How amazing!The programmer is a genius! "
date:       2016-06-22
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-a995adb879946d2d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - CSS

---

> 很多时候最不能相信的就是你的眼睛。

今天在网易云的网页版听歌，话说Steve Vai的曲子永远是这么让人揣摩不透，不过我还时更喜欢老Joe，咦，跑题了···

![](http://images2015.cnblogs.com/blog/929120/201606/929120-20160622141525235-1632127211.png)

大家可以看到评论输入框和回复框，上面都有个小尖角，实现的方式有很多，我一般是用border来做，只要给一个元素加上这四条属性就行了：

```
border-top: 400px solid red;
border-right: 400px solid transparent;
border-bottom: 400px solid transparent;
border-left: 400px solid transparent;
```

下面要讲的是网易云上面的黑科技，我看完真的是服···

作为一个程序猿，看网页总喜欢手贱的审查元素...

![](http://images2015.cnblogs.com/blog/929120/201606/929120-20160622142259547-420713142.png)

咦？这两个小黑块是啥？稍微一想，原来是这样....

顶层的小方块颜色是白色背景颜色，下面还层叠了一个背景颜色为边框颜色的小方块，还是上图比较直观：

![](http://images2015.cnblogs.com/blog/929120/201606/929120-20160622145114469-397586137.png)

这里有两个小方块，我们两个小方块都position:absolute;把右边的小方块向左移，移到马上覆盖左边方块为止：

![](http://images2015.cnblogs.com/blog/929120/201606/929120-20160622145402953-873575.png)

OK，就像这个样子，聪明的你可能已经知道这个是什么了，假定背景颜色是白色的，边框是红色的，那我们只需要改变着两个元素的color属性即可：

![](http://upload-images.jianshu.io/upload_images/2859850-aae2fc70b22d91c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们只需给父元素position:relative;把这两个小方块定位到相应的地方就OK啦，感觉能想到这种方法的人也挺牛的，啊哈。

> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
