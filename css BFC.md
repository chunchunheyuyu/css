![射手.jpg](https://upload-images.jianshu.io/upload_images/10758861-16e68b2dcf1783f8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**视觉格式化模型(visual formatting model)**是用来处理文档并将它显示在视觉媒体上的机制，它也是CSS中的一个概念。


视觉格式化模型定义了盒（Box）的生成:
> 1.块盒 block box
2.行内盒 inline box
3.匿名盒 anonymous box

**块盒（block box）**

- 当display属性值为block，table，list-item时，它是块级元素 block-level
 - 视觉上呈现为块，竖直排列；
- 块级盒参与(块格式化上下文)；
- 每个块级元素至少生成一个块级盒，称为主要块级盒(principal block-level box)。

**行内盒（inline box）**

- 当display属性值为inline，inline-block，inline-table时，它是行内级元素
 - 视觉上它将内容和其他行内级元素排列为多行，如段落内容，图片等
- 行内盒参与(行内格式化上下文)inline formatting context；

**匿名盒（anonymous box）**
- 匿名盒也有份匿名块盒与匿名行内盒，因为匿名盒没有名字，不能利用选择器来选择它们，所以它们的所有属性都为inherit或初始默认值；
##定位方式
在定位时，浏览器就会根据元素的盒类型和上下文对元素进行定位。主要为三种
>1.常规流
2.浮动
3.绝对定位

**常规流**

- 常规流中，盒子一个接着一个排列
- 块级格式化上下文中，为竖着排列
- 行内级格式化上下文中，为横着排列
- posihuotion为static或relative,并float为none时，触发常规流

**浮动**

- 盒称为浮动盒floating boxes
- 导致常规流环绕在它的周围，除非设置clear属性

**绝对定位**

- 盒从常规流中被移除，不影响常规流布局
- 它的定位相对于它的包含块： top bottom left right
- position:absolute,它是绝对定位元素，元素定位相对于最近的一个relative、fixed或absolute的父元素，都没有则相对于body

###BFC
BFC全称是Block Formatting Context，即块格式化上下文。

BFC创建方法
- 浮动，float不为none
- 绝对定位元素，position:absolute或fixed
- 行内块 display:inline-block
- 表格单元格 display:table-cell
- overflow的值不为visible的元素
- 弹性盒flex boxes

BFC的约束规则

- 内部的Box会在垂直方向上一个接一个的放置
- 垂直方向的距离有margin决定(属于同一个BFC的两个相邻Box的margin会发生重叠，与方向无关)
- 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此
- BFC的区域不会与float的元素区域重叠
- 计算BFC的高度时，浮动子元素也参与计算
- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面元素，反之亦然

###BFC的作用
1. 不和浮动元素重叠
```<style>
        .right{
             width: 300px;
             height: 300px;
             background-color: blueviolet;
         
        }
        .left{
              width: 50px;
              height: 50px;
              background-color:springgreen;
              float: left;
        }
    </style>
</head>
<body>
 
        <div class="left"></div>
        <div class="right"></div>
  
</body>
</html>

```
![BFC-浮动.png](https://upload-images.jianshu.io/upload_images/10758861-c63c9f205dd21d7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
      .right{
             width: 300px;
             height: 300px;
             background-color: blueviolet;
             overflow:hidden;<!-- 触发BFC特性，不与浮动重叠-->
        }
```
![BFC-overflow.png](https://upload-images.jianshu.io/upload_images/10758861-ee982fe6083d90b0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2.  清除浮动
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>BFC</title>
    <style>
        .right{
             width: 300px;
             height: 300px;
             background-color: blueviolet;
             float: ;
        }
        .left{
              width: 50px;
              height: 50px;
              background-color:springgreen;
              float: left;
        }
        .root{
            border: 5px solid deeppink;
            width: 600px;
        }
    </style>
</head>
<body>
    <div class="root">
        <div class="left"></div>
        <div class="right"></div>
    </div>

</body>
</html>
```
![塌陷.png](https://upload-images.jianshu.io/upload_images/10758861-8eeb9863941bf067.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
 .root{
            border: 5px solid deeppink;
            width: 600px;
            overflow: hidden; /* 触发BFC,清除浮动 */
        }
   
```
![BFC-清除浮动.png](https://upload-images.jianshu.io/upload_images/10758861-eb0aa5a726205cd6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


3. 防止垂直 margin 重叠
```
<style>
        p {
            color: #f55;
            background: yellow;
            width: 200px;
            line-height: 100px;
            text-align:center;
            margin: 100px;
        }
    </style>
<body>
    <p>春夏秋冬</p>
    <p>梅兰竹菊</p>
</body>
```
![margin重叠.png](https://upload-images.jianshu.io/upload_images/10758861-ca4c46cbec845a86.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
>因为同属于一个BFC margin在垂直方向重合


>再创建一个BFC
```
   <style>
        p {
            color: #f55;
            background: yellow;
            width: 200px;
            line-height: 100px;
            text-align:center;
            margin: 100px;
        }
        .root{
            overflow: hidden;
        }
    </style>
<body>
    <div class="root">
        <p>春夏秋冬</p>
    </div>

    <p>梅兰竹菊</p>
</body>
```
![2个BFC.png](https://upload-images.jianshu.io/upload_images/10758861-bd6663950b93ba1b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


