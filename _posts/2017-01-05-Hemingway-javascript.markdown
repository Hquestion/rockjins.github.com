---
layout: post
title: ' 『翻译』如果让海明威写JavaScript '
subtitle: ' How amazing！ '
date: 2017-01-05
author: Shock
header-img: '/upload-images.jianshu.io/upload_images/2859850-0a0e4dc3cabc9214.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240'
catalog: true
tags:
  - translation
---

> 原文链接：[http://byfat.xxx/if-hemingway-wrote-javascript](http://byfat.xxx/if-hemingway-wrote-javascript)

在写第一行代码很久以前，我就酷爱文学。现在，我写JavaScript，不计其数。我正在写一本关于JavaScript的书。

JavaScript凭啥能吸引那么多文艺青年？说到它有限的语法所具备的表达潜能，我倒是有几点不成熟的想法，不过那是另外一个话题了。哎，如果那些大作家都喜欢上JavaScript，会咋样？你说他们会用JavaScript写出点什么东西来？作为海明威的十足拥趸，我的第一反应也是这老爷子不可能喜欢编程序（包括程序员）。话虽如此，我还是愿意相信在对它的各种非议中，其实潜藏着足以打动人心的一点：它是一门很文艺的语言，你说呢？它表面上简单粗陋、平淡无奇，而实质上却引人入胜、内涵十足。

## 代码审查之母

![](http://upload-images.jianshu.io/upload_images/2859850-0ffb33a8d91775dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

前些天，我做了一个梦。梦见我让海明威还有其他四位作家给我写点JavaScript，特别是得写一个能返回*指定长度斐波纳契数列的函数*。我发现这些作家解决问题的方法各有千秋，很有意思。不过确实都写得不错，至少都实现了既定的功能（连安德烈·布勒东都写出来了）。下面就是他们交给我的作业。

### 欧内斯特·海明威（美国作家）

```javascript
function fibonacci(size) {

  var first = 0, second = 1, next, count = 2, result = [first, second];

  if(size < 2)
    return "the request was made but it was not good"

  while(count++ < size) {
    next = first + second;
    first = second;
    second = next;
    result.push(next);
  }
  return result;
}
```

毫不奇怪。海明威的代码非常凝练，没有浪费一个词一个变量。代码没什么出奇之处，甚至显得有点迂腐，可这正是海明威作品的长处。没有烦琐的逻辑，也没有花里胡哨的变量名。就那么简单直白地把活儿干了，干完完事儿。

海明威没心情跟傻瓜逗闷子，如果你想要的是一个长度小于2的数列，他根本不睬你：“我累啦，你的问题很白痴。”

### 威廉·莎士比亚（英国诗人、作家）

```javascript
function theSeriesOfFIBONACCI(theSize) {

  //a CALCKULATION in two acts.
  //employ'ng the humourous logick of JAVA-SCRIPTE

  //Dramatis Personae
  var theResult; //an ARRAY to contain THE NUMBERS
  var theCounter; //a NUMBER, serv'nt to the FOR LOOP

  //ACT I: in which a ZERO is added for INITIATION

  //[ENTER: theResult]

  //Upon the noble list bestow a zero
  var theResult = [0];

  //ACT II: a LOOP in which the final TWO NUMBERS are QUEREED and SUMM'D

  //[ENTER: theCounter]

  //Commence at one and venture o'er the numbers
  for (theCounter = 1; theCounter < theSize; theCounter++) {
    //By divination set adjoining members
    theResult[theCounter] = (theResult[theCounter-1]||1) + theResult[Math.max(0, theCounter-2)];
  }

  //'Tis done, and here's the answer.
  return theResult;

  //[Exuent]
}
```

这位文豪啰嗦了点，可也是独树一帜了。注意他的注释（不算场名和台本），典型的英文抑扬格五音步格律——共十对音节，每音步（两个音节）的重音都落在第二个音节上。在他的戏剧中，莎士比亚经常会脱离严格的抑扬格五音步格律以示强调，比如增加一个音节，或者采用交替重音。在这个编程作业中，他好像也运用了同样的技巧。码如其文。

### 安德烈·布勒东（Andre Breton，法国诗人和评论家，超现实主义创始人之一）

```javascript
function Colette(umbrella) {
  var staircase = 0, galleons = 0, brigantines = 1, armada = [galleons, brigantines], bassoon;
  Array.prototype.embrace = [].push;

  while(2 + staircase++ < umbrella) {
    bassoon = galleons + brigantines;
    armada.embrace(brigantines = (galleons = brigantines, bassoon));
  }

  return armada;
}
```

作为超现实主义运动的倡导者，布勒东主张梦想比现实更有趣，应该作为创作的出发点。他的变量命名颇具超现实主义色彩。尽管并非无可挑剔，但他的作品的确几近完美，真挚又美好。在他有意识的表达中，蕴含着一幅无意识的梦幻图景。可以把这个作业看成华美诗篇Facteur Cheval的再创作。

布勒东在这个斐波纳契函数中总是喜欢使用老相好的名字，他把结果想象成了一个史前舰队。他的方案逻辑优雅，巧妙地采用了逗号运算符在galleons、brigantines和bassoons之间同时迁移元素。向安德烈致敬！

### 罗贝托·波拉尼奥（Roberto Bolano，智利诗人和小说家）

```javascript
function LeonardoPisanoBigollo(l) {

  if(l < 0) {
    return "I'd prefer not to respond. (Although several replies occur to me)"
  }

  /**/

  //Everything is getting complicated.
  for (var i=2,r=[0,1].slice(0,l);i<l;r.push(r[i-1]+r[i-2]),i++)

  /**/

  //Here are some other mathematicians. Mostly it's just nonsense.

  rationalTheorists = ["Archimedes of Syracuse", "Pierre de Fermat (such margins, boys!)", "Srinivasa Ramanujan", "Rene Descartes", "Leonhard Euler", "Carl Gauss", "Johann Bernoulli", "Jacob Bernoulli", "Aryabhata", "Brahmagupta", "Bhaskara II", "Nilakantha Somayaji", "Omar Khayyám", "Muhammad ibn Mūsā al-Khwārizmī", "Bernhard Riemann", "Gottfried Leibniz", "Andrey Kolmogorov", "Euclid of Alexandria", "Jules Henri Poincaré", "Srinivasa Ramanujan", "Alexander Grothendieck (who could forget?)", "David Hilbert", "Alan Turing", "von Neumann", "Kurt Gödel", "Joseph-Louis Lagrange", "Georg Cantor", "William Rowan Hamilton", "Carl Jacobi", "Évariste Galois", "Nikolay Lobachevsky", "Rene Descartes", "Joseph Fourier", "Pierre-Simon Laplace", "Alonzo Church", "Nikolay Bogolyubov"]

  /**/

  //I didn't understand any of this, but here it is anyway.
  return r

  /**/

  //Nothing happens here and if it does I'd rather not talk about it.
}
```

如果这辈子没看过波拉尼奥的著作，那你的生命是不完整的。波拉尼奥的作品忽而精于事故，忽而憨态可掬，让人叹为观止。他的叙事风格以毫无悬念的坦诚见长。人类的弱点始终存在，但温暖幽默地传达出每一个弱点，却无不令人沉醉、催人振奋。

一如既往，他的编程作业也流露出了一种不安、局促和无知。他给出的解答尽管颇显才情，可总让人觉得有几分累赘。偏执依旧，跑题依旧，他好像更愿意向我们展示似乎很有意思，但其实毫无用处的天才数学家名录。

以下几方面也是波拉尼奥的特点，比如长短段并列、忘记加分号（对应着他小说中缺失的引号），以及隐含地使用全局变量——暗示每个变量注定会在后续章节中再次现身。

### 查尔斯·狄更斯

```javascript
function mrFibbowicksNumbers(enormity) {
  var assortment = [0,1,1], tally = 3, artfulRatio = 1.61803;

  while(tally++ < enormity) {
    //here is an exceedingly clever device
    assortment.push(Math.round(assortment[tally-2] * artfulRatio));
  }

  //should there be an overabundance of elements, a remedy need be applied
  return assortment.slice(0, enormity);
}
```

我不是狄更斯的粉丝。我基本同意亨利·詹姆斯（美国著名小说家和批评家）的恶评：

“要是让我们冒险评价一下他的文学成就，可以称他为最肤浅的小说家。没错，这么说等于把它归入了他所处的文学领域的低等行列，但我们愿意承认这一点。把狄更斯先生归入最伟大的小说家之列，我们是过意不去的。因为他除了人物角色，并没有创造其他任何东西。他没有对我们理解人物角色多给任何资料。”

——亨利·詹姆斯谈查尔斯·狄更斯，评《我们共同的朋友》，1865年12月21日

他的肤浅从他的斐波纳契作业中可见一斑。没错，变量名还算中规中矩，但却是他无法把握实质性内容和内心理解不到位的表现。他没有从实质上领会斐波纳契数列的含义，倒是一心想通过乘法解决问题。哎。

## 最终点评

不管是老道（Crockford）的极力维护，还是干巴巴的计算机科学课，条条框框始终是JavaScript的敌人。有些开发者喜欢手册和样板，结果就是Java。JavaScript的趣味性源自它天性就不刻板，以及由此生发的无限可能。自然语言也具有相似的特点。最好的作者和最优秀的JavaScript开发者一定会对这门语言神魂颠倒，没有一天不在探索和实践它，从而塑造自己的风格、自己的习惯，还有自己的表达方式。

就这些，希望你喜欢。恐怕大都是无稽之谈。
