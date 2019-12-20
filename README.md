#css

Cascading Style Sheet 层叠样式表

###[css选择器](./css选择器.md)

###盒模型
盒模型有两种，IE怪异盒子模型/W3C标准盒子模型；

盒模型是由：内容(content)/内边距(padding)/边框(border)/外边距(margin)组成的。

标准模型的宽高是指的是content区宽高;
IE盒模型的宽高是指的content+padding+border的宽高.

![W3C盒模型](./img/stadardBox.png)

![IE盒模型](./img/strangeBox.png)

### css如何设置这两种盒模型

标准盒模型：
```
box-sizing:content-box;
```
怪异盒模型
```
box-sizing:border-box;
```

###BFC
[什么是BFC](https://www.cnblogs.com/libin-1/p/7098468.html)

W3C对BFC定义：
> 浮动元素和绝对定位元素，非块级盒子的块级容器(例如inline-blocks,table-cells和table-captions),以及overflow值不为"visiable"的块级盒子，都会为他们的内容创建新的BFC(块级格式上下文)。

BFC(Block formatting content)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box 参与，它对丁了内部的Block-level Box 如何布局，并且与这个区域外部毫不相干。


BFC作用：
1. 利用BFC避免外边距折叠
2. 清除内部浮动(撑开高度)
   1. 原理：触发父div的BFC属性，使下面的子div都处在父div的同一个BFC区域之内
3. 避免文字环绕
4. 分属于不同的BFC时，可以阻止margin重叠
5. 多列布局中使用BFC

如何生成BFC:（脱离文档流，满足下列的任意一个或多个条件即可）
1. 根元素，即HTML元素(最大的一个BFC)
2. 属于同一个BFC的两个相邻的Box的margin会发生重叠
3. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此，文字环绕效果，设置float
4. BFC的区域不会与float box 重叠
5. 计算BFC的高度，浮动元素也参与计算


### BFC/IFC/GFC和FFC
- BFC(Block formatting contexts):块级格式上下文
- IFC(Inline formatting contexts):内联格式上下文
- GFC(GrideLayout formatting contexts):网络布局格式化上下文
- FFC(Flex formatting contexts):自适应格式上下文

### 非布局样式
- 字体/字重/颜色/大小/行高
- 背景/边框
- 滚动/换行
- 粗体/斜体/下划线
- 其他

### 行高的构成
- 行高是由 line-box 组成的
- line-box 是由一行里的 inline-box 组成的
- inline-box 种最高的那个，或字体最大的那个决定行高

### float 
- 元素"浮动"
- 脱离文档流
- 不脱离文档流
- 位置尽量靠上，并靠左或右

对自己的影响
- 形成"块"(BFC)
- 这个块会负责自己的布局，宽高由自己决定

比如 span 中用 float 这个span就形成了一个BFC，就可以设置宽高了

对兄弟元素的影响
- 上面一般贴非float元素
- 靠边贴float元素或边
- 不影响其他块级元素位置
- 影响其他块级元素文本

对父级元素的影响
- 从布局上"消失"
- 高度塌陷

### 清除浮动
浮动的元素布局时不会占据父元素的布局空间，即父元素布局时不会管浮动元素，浮动元素有可能超出父元素，从而对其他元素造成影响。

方法一：让父元素变为一个BFC。
父元素 overflow:auto/hidden.让父元素区关注里面的高度
必须定义width或者zoom:1,同时不能定义height,使用overflow:auto时，浏览器会自动检查浮动区域的高度。

方法二：使用伪元素清除浮动
```css
.container::after{
    content:"";
    clear:both;
    display:block;
    visibility:hidden;
    height:0;
}
```

### inline-block的间隙
两个并列的inline-block中间会有一条裂缝，这个的原因是两个标签之间有空格，浏览器把这些空格当成文字中空格，所以这两个块中间多少间隙。

解决办法：
1. 删除两个标签间的空格，但是这样html排版不好
2. 容器元素font-size:0 然后再在里面重新设置字体大小

### 你对line-height 是如何理解的？

- line-height 指一行字的高度，包含了字间距，实际上是下一行基线到上一行基线的距离
- 如果一个标签没有定义height属性，那么其最终表现的高度是由line-height 决定的
- 一个容器没有设置高度，那么撑开容器高度的是 line-height 而不是容器内的文字内容
- 把line-height 值设置为height 一样大小的值可以实现单行文字的垂直居中
- line-height 和 height 都能撑开一个高度，height会触发haslayout(一个低版本的IE的东西)，而line-height不会
  



















