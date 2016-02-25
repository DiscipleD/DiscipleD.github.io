---
layout: post
title: CSS3 Flex Box
tags: [CSS3, Flex]
categories: [Css]
---

##What is Flex?
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

W3C于2009年提出了这一方案，时至今日，常用的浏览器已经全部都提供了对它的支持（当然不包括IE8）。  
![Flex浏览器支持情况](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071003.jpg)

##Why to use Flex?
简便的实现页面布局。

##How to use Flex?
为一个元素简单地设置 display: flex; 就使得其成为Flex容器（flex container），其内部的所有子元素自动成为容器中的成员（flex item）。

容器默认存在两根轴：水平的主轴（`main axis`）和垂直的交叉轴（`cross axis`）。主轴的开始位置（与边框的交叉点）叫做（`main start`），结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

项目默认沿主轴水平排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。
![Flex基本概念](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)


**注意：**

当一个元素设置为 display: flex; 后， 其子元素（即flex item）的float，clear和vertical-align属性将无效。

对于Webkit内核的浏览器需要加上`-webkit`前缀。

##Flex Container Attributes
----
1. `flex-direction`: row | row-reverse | column | column-reverse;  
该属性决定flex item在容器中的排列方向，默认为row，即水平从左 → 右排列；column为从 上 ↓ 下排列；加-reverse后缀，即和原先排列顺序相反。
2. `flex-wrap`: nowrap | wrap | wrap-reverse;  
该属性决定flex item在容器中是否换行，换行的方式又是什么，默认为nowrap，即不换行。wrap为换行，当`flex-direction`为row时，内容从 上 ↓ 下按行排列；当`flex-direction`为column时，内容从 左 → 右按列排列；加-reverse后缀，即和原先排列顺序相反。
3. `flex-flow`: <flex-direction> || <flex-wrap>  
该属性是`flex-direction`和`flex-wrap`的简写形式，默认值是原属性`flex-direction`和`flex-wrap`的默认值，即row nowrap。
4. `justify-content`: flex-start | flex-end | center | space-between | space-around;  
该属性决定flex item在行内的水平对齐方式或列内的垂直对齐方式，默认值是flex-start。  
flex-start： 与轴的start对齐，即左对齐(flex-direction: row)，上对齐(flex-direction: column)  
flex-end：与轴的end对齐，即右对齐(flex-direction:row)，下对齐(flex-direction:column)  
center： 与轴的的中点对齐  
space-between：与轴的两端对齐，flex-item之间的间隔都相等，头尾的flex item紧贴轴的start位置  
space-around：每个flex item两侧的间隔相等。所以，flex item之间的间隔比flex item与轴的start之间的间隔大一倍  
**注意：**  
flex item默认是没有间距的，间距是由flex container的宽度或高度与flex item的宽度或高度之间的差产生的，即如果flex container的宽度为1000px，flex item的宽度为100px，container下有10个item，那无论justify-content设任何的值，展示都将是10个item紧贴地并列排列，item与item之间没有任何间隙。
5. `align-items`: flex-start | flex-end | center | baseline | stretch;  
该属性与justify-content相反，决定flex item在行内的垂直对齐方式或列内的水平对齐方式，默认值是stretch。  
flex-start：与轴的start对齐  
flex-end：与轴的end对齐  
center：与轴的的中点对齐  
baseline： 与flex item的第一行文字的baseline对齐  
stretch：如果flex item未设置宽度或高度或设为auto，将占满这行的高度或这列的宽度  
**注意：**  
baseline属性在container的flex-direction设置为column时无效。  
当align-items属性值设置为stretch时，如一个flex item设置了宽度或高度，则这个flex item应用flex-start，且只对该flex item生效。  
6. `align-content`: flex-start | flex-end | center | space-between | space-around | stretch;  
该属性类似于`justify-content`属性，与之不同的是，该属性决定flex item每行或每列在flex container下的对齐方式，如果flex item只有一行或一列，则该属性无效，默认值为stretch。
flex-start：与轴的start对齐  
flex-end：与轴的end对齐  
center：与轴的中点对齐  
space-between：与轴的两端对齐，轴线之间的间隔都相等 
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍  
stretch：轴线占满整个交叉轴  
**注意：**  
当`align-content`属性设定为flex-start、flex-end或center时，轴与轴之间默认是没有间隔的。

##Flex Item Attributes
----
1. `order`: \<integer\>;  
该属性定义flex item的排列顺序，数值越小，排列越靠前，默认值为0。  
**注意：**数值可以为负数。
2. `flex-grow`: \<number\>;  
该属性定义flex item的放大比例，默认值为0，即使有空余空间也不放大该元素。  
**注意：**数值可以为小数，但不能为负数。
3. `flex-shrink`: \<number\>;  
该属性与`flex-grow`相反，定义flex item的缩小比例，默认值为1，即空间不足时，等比例缩小元素；flex-grow为0，则空间不足时也不缩小该元素。  
**注意：**数值可以为小数，但不能为负数。
4. `flex-basis`: \<length\> | auto;  
该属性定义在分配剩余空间之前，flex item占所在轴的大小，默认值为auto，即原有元素大小。  
**注意：**该属性设定的大小为未分配剩余空间之前的大小，flex item最终显示的大小会受flex-grow或flex-shrink的影响。
5. `flex`: auto | none | [ <`flex-grow`> <`flex-shrink`>? || <`flex-basis`> ];  
该属性是`flex-grow`、`flex-shrink`和`flex-basis`的简写，默认值为各属性的默认值，0 1 auto。  
该属性还有2个快捷值：auto(1 1 auto), 即flex item根据container的内容大小自动缩放；none(0 0 auto)，即flex item保持自身元素大小，不进行缩放。
6. `align-self`: auto | flex-start | flex-end | center | baseline | stretch;  
该属性用来设置只用于自身的对齐方式，将覆盖container的`align-items`属性，默认值为auto，即继承父属性的`align-items`属性。

##TRY
----
俗话说的好，光说不练假把式，既然已经清楚了概念，我就尝试使用这些特性，看到阮老师的另一篇文章后，自己也尝试做了一遍，通过flex完成了骰子的6个面。  
![骰子的六面](http://i.imgur.com/kx3NmeS.png)[点击查看源码](http://plnkr.co/edit/BthfuHwFAlZiOUxrU99v?p=preview)

如果理解了flex容器的特性，那么上面的列子尝试起来并不难，只有在第5点的时候遇到一些小障碍，如何画中间那个点，最后是通过给第3个点增加两边的margin，使元素的宽度增加来处理。如果你也对这个有兴趣可以参考[这里](https://davidwalsh.name/flexbox-dice)，里面也有几种不同的实现，或许对你也有所启发，如果你有更好的想法，欢迎留言交流。

另外，在查资料时还发现CSS3 box-flex，一看描述和内容，完全和flex是同一个东西啊。

* `display: box`：弹性模型第一版，不推荐使用（适用于老版本浏览器）。  
* `display: flexbox`：box升级版，不推荐使用（适用于老版本浏览器）。  
* `display: flex`：最新的弹性模型版本，推荐使用。  

参考资料：  
1. [阮一峰 Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)  
2. [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/#flexbox-basics)  
3. [阮一峰 Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)  
4. [Getting Dicey With Flexbox](https://davidwalsh.name/flexbox-dice)