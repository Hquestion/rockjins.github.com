---
layout:     post
title:      " 三角函数学习历程记录 "
subtitle:   " trigonometric function. "
date:       2017-01-19
author:     "Shock"
header-img: "/upload-images.jianshu.io/upload_images/2859850-e7dfe46f2c5c5d87.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240"
catalog: true
tags:
    - JavaScript
    - Math

---

>  是时候捡起来了 别那么在乎别人的眼光

### 1.已知斜边为20，邻边为10，求角x.

![](http://upload-images.jianshu.io/upload_images/2859850-d8ba565406f20742.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`Math.acos(10/20)/(Math.PI/180);`

---

### 2.已知C是45°，斜边为20，求其邻边x.

![](http://upload-images.jianshu.io/upload_images/2859850-13de06296d5a1fc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`Math.cos(45*Math.PI/180)*20;`

---

### 3.已知A是55°，对边为20，求其邻边x.

![](http://upload-images.jianshu.io/upload_images/2859850-d51b786e69a9e791.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`20/Math.tan(55*(Math.PI/180));`

---

### 4.已知角B为60°，AC长为8，AB长为5，求角C的正弦.

![](http://upload-images.jianshu.io/upload_images/2859850-4f1e642f69ad1d8a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`5/(8/Math.sin(60*(Math.PI/180)));`

---

### 5.已知C大小为120°,B大小为30°,AC=6,求AB长x.

![](http://upload-images.jianshu.io/upload_images/2859850-52b7cc219653f989.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`(6/Math.sin(30*(Math.PI/180)))*Math.sin((180-120)*(Math.PI/180));`

---

### 6.△ABC中，A,B,C所对的边为a,b,c。角B=30°，AB=9，AC=3√3，求角C的大小.

![](http://upload-images.jianshu.io/upload_images/2859850-2b54e1a28ac19b84.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`Math.asin(9/((3*Math.sqrt(3))/Math.sin(30*(Math.PI/180))))/(Math.PI/180);`

Tips :因为sin(C) = sin(180° - C)，所以有两个解，60°和120°。

当然也不是一定就有两个解，如果B+C>180°那肯定是不行的，就像这种题：

![](http://upload-images.jianshu.io/upload_images/2859850-0ab1ee7e8cec9b21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

学生时代考试就经常忘记有多个解，有木有！！！

---

### 7.已知AB=5,BC=8,角B=60°，求x.

![](http://upload-images.jianshu.io/upload_images/2859850-e2a1a7ae297353c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`Math.sqrt(Math.pow(5,2)+Math.pow(8,2)-(2*5*8*Math.cos(60*(Math.PI/180))));`

---

### 8.已知三边长为3,7,8，求边长为7的AC边所对的角B大小.

![](http://upload-images.jianshu.io/upload_images/2859850-1831f6002ad1b20a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

答：`Math.acos((Math.pow(3,2)+Math.pow(8,2)-Math.pow(7,2))/(2*3*8))/(Math.PI/180);`

> 本文出自[Rockjins Blog](https://rockjins.github.io)，转载请与作者联系。否则将追究法律责任。
