![女.jpg](https://upload-images.jianshu.io/upload_images/10758861-deb0e5d022b149f3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#浮动 
浮动元素会**脱离文档流**并按照float的属性浮动，直到碰到父元素或者另一个浮动元素

#浮动的特性


- **浮动会脱离文档流** 
![都不浮动.png](https://upload-images.jianshu.io/upload_images/10758861-1564c7ac4f0827c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![1号左浮动.png](https://upload-images.jianshu.io/upload_images/10758861-6c6c04d4abecaada.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


 由上二图可知，默认三个设置了宽高的block元素，本来会格子独占一行。1号选手设置了浮动后，会脱离文档流，直到碰到父元素，**遮挡普通元素**（把2号选手遮挡）

- **浮动元素之间可排列** 
![集体左浮动.png](https://upload-images.jianshu.io/upload_images/10758861-0d6a5f494256de33.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![集体右浮动.png](https://upload-images.jianshu.io/upload_images/10758861-9b3e9b67f2968efb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![浮动卡主.png](https://upload-images.jianshu.io/upload_images/10758861-f31bcf1207e34bcc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

浮动会向左/向右浮动，直到碰到另一个浮动元素或父元素为止。浮动可以设置宽高，并且能够一行多个。
- **浮动会导致父元素高度坍塌** 
当父元素中只有浮动元素，而浮动元素脱离了文档流，并不占据文档流的位置，自然父元素也就不能被撑开，所以没了高度。
![父元素高度塌陷.png](https://upload-images.jianshu.io/upload_images/10758861-9a1695f4cd734ec0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#清除浮动
###clear方式清除浮动
####clear
clear属性可设置，其左右不允许出现浮动元素
```
<div class="root">
        <div class="fly-1">1号选手</div>
        <div class="fly-2">2号选手</div>
        <div class="fly-3">3号选手</div>
        <div class="empty"></div><!--添加一个空元素，为其添加clear属性 -->
 </div>
 <style>
  .empty{
            clear: both;
        }
  
</style>      
```
![clear-both.png](https://upload-images.jianshu.io/upload_images/10758861-eb5aca0af2229d4c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


高度坍塌的问题解决了

- **clear清除浮动套路** 
```
// 现代浏览器clearfix方案，不支持IE6/7
.clearfix:after {
    display: table;
    content: " ";
    clear: both;
}

// 全浏览器通用的clearfix方案
// 引入了zoom以支持IE6/7
.clearfix:after {
    display: table;
    content: " ";
    clear: both;
}
.clearfix{
    *zoom: 1;
}

// 全浏览器通用的clearfix方案【推荐】
// 引入了zoom以支持IE6/7
// 同时加入:before以解决现代浏览器上边距折叠的问题
.clearfix:before,
.clearfix:after {
    display: table;
    content: " ";
}
.clearfix:after {
    clear: both;
}
.clearfix{
    *zoom: 1;
}


```
###BFC清除浮动
BFC全称是块状格式化上下文，它是按照块级盒子布局的。

**BFC的主要特征**
 - 不和浮动元素重叠。
 -  清除元素内部浮动(可解决高度塌陷问题)
 -  防止垂直 margin 重叠


**BFC的触发方式**

我们可以给父元素添加以下属性来触发BFC：

✦ float 为 left | right
✦ overflow 为 hidden | auto | scorll
✦ display 为 table-cell | table-caption | inline-block | flex | inline-flex
✦ position 为 absolute | fixed**
