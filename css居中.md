![狮子.jpg](https://upload-images.jianshu.io/upload_images/10758861-1076e0be1621595e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##水平居中
- 内联元素 display：inline；
使用text-align：center

- 块级元素display：block；
######已定宽高的块级元素
使用margin：auto；
>margin法
需要满足三个条件:
1.元素**定宽**
2.元素为块级元素或行内元素设置**display:block**
3.元素的margin-left和margin-right都必须设置为**auto**
######不定宽高的块级元素
1:在元素外加入 table 标签（完整的，包括 table、tbody、tr、td），该元素写在 td 内，然后设置 margin 的值为 auto；
2:给该元素设置 display:inine 方法；
3:父元素设置 position:relative 和 left:50%，子元素设置 position:relative 和 left:50%



- flex布局居中
```
display: flex;
justify-content: center;
```

##垂直居中
- position:absolute（fixed）,设置left、top、margin-left、margin-top的属性
```
.center{
           width: 150px;
           height: 150px;
           position: absolute;/* 也可以fixed*/
           top:50%;
           left: 50%;
           margin-top: -75px;
           margin-left: -75px;
           border: navy 5px solid;
       }

.center{
          width: 150px;
          height: 150px;
          background: red;
          position: absolute;/*或fixed*/
          top:0;
          right:0;
          bottom:0;
          left:0;
          margin: auto;
}


      /* 适用于定宽定高元素*/
```
- display:table-cell
```
  <div class="box">
        <p>好好学习，天天向上</p>
  </div>

  .box{
           display: table-cell;
           vertical-align: middle;
           background: #00aaaa;
           width: 50px;
           height: 50px;
       }
```
- css3的新属性transform:translate(x,y)属性
```
.center{
     position: absolute;
     position: absolute;
     top:50%;
     left:50%;
     transform: translate(-50%,-50%);
     -webkit-transform: translate(-50%,-50%);/* Safari 和 Chrome */
     -moz-transform: translate(-50%,-50%);/* Firefox */
     -ms-transform: translate(-50%,-50%);/* IE 9 */
  }
 /* 适用于不定宽高元素*/
```
- flex布局
```
.box{
    display: -webkit-box;
    display: -webkit-flex;
    display: -moz-box;
    display: -moz-flex;
    display: -ms-flexbox;
    display: flex;
    /*水平居中*/
    -webkit-box-align: center;
    -moz-box-align: center;
    -ms-flex-pack:center;
    -webkit-justify-content: center;
    -moz-justify-content: center;
    justify-content: center;
    /*垂直居中*/
    -webkit-box-pack: center;
    -moz-box-pack: center;
    -ms-flex-align:center;
    -webkit-align-items: center;
    -moz-align-items: center;
    align-items: center;
}
 /* 适用于不定宽高元素*/
```
- 使用伪类
```
.box{
    display: block;
    background: red;
    height: 100px;
}
.center::before{
    content: '';
    display: block;
    vertical-align: middle;
    height: 100%;
}
.center::after{
    content: '';
    display: block;
    vertical-align: middle;
    height: 100%;
}
.box .center{
    height: 33px;
    line-height: 33px;
    text-align: center;
}


```