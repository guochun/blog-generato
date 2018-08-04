---
title: 用CSS如何画太极图
date: 2018-08-04 17:51:03
tags: CSS
---

太极图是指代表阴阳（太极）思想的中国符号，有时也泛指历史上其他文化中所使用的与中国太极图相似的几何图案。  

这类符号标志大部分是由两个不同颜色的半圆形泪珠状曲线组成，称为黑白阴阳双鱼。  

废话少说对于程序员来说我们是用代码交流的人群直接用代码说话。

首先先用一张太极图压压惊:
    
 ![太极](https://gss0.baidu.com/9fo3dSag_xI4khGko9WTAnF6hhy/zhidao/wh%3D600%2C800/sign=0924f945805494ee8777071f1dc5ccc6/6159252dd42a2834ce614ef157b5c9ea14cebf01.jpg)    
     
​     
**1 第一种方法:** 
    
html结构:     
    
```
    <div id="yinyang">
      <div class="yin">
        <div class="yang-inner"></div>
      </div>
      <div class="yang">
        <div class="ying-inner"></div>
      </div>
  </div>
```
css结构：   
    
```
/*添加一个灰色的背景*/
body{
  background: #eee;
}
/*画出八卦图的整体部分*/
#yinyang {
  
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background: linear-gradient(to bottom, #ffffff 0%,#ffffff 50%,#000000    52%,#000000 100%); 
  position:relative;
  margin: 200px auto;
}
/*八卦的黑色圆环叠加到整体的内部形成半圆形泪珠*/
#yinyang .yin {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: #000;
  position: absolute;
  top: 50px;
  left:0;
}
/*画出内部的白色小圆环*/
#yinyang .yin .yang-inner {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
  position: absolute;
  top: 40px;
  left: 40px;
}
/*八卦的白色圆环叠加到整体的内部形成半圆形泪珠*/
#yinyang .yang {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: #fff;
  position: absolute;
  top: 50px;
  right: 0;
}
/*画出内部的黑色的小圆环*/
#yinyang .yang .ying-inner {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: #000;
    position: absolute;
    top: 40px;
    left: 40px;
}

```
**2 第二种方法**  

html结构

```
    <div id="yinyang"></div>
```
 css结构

```
/*画出八卦的整体*/
#yinyang{
  width: 196px;
  height: 98px;
  border-radius: 50%;
  border-top: 2px solid black;
  border-left: 2px solid black;
  border-right: 2px solid black;
  border-bottom:100px solid black;
  background: #fff;
  position: relative;
  
}

/*伪类画出八卦的黑色的部分*/
#yinyang::before{
  
  content: "";
  display:block;
  width: 20px;
  height: 20px;
  border: 40px solid #000;
  background: #fff;
  border-radius: 50%;
  position: absolute;
  top:50px;
  
}

/*伪类画出八卦的白色的部分*/
#yinyang::after {
  content: "";
  display:block;
  width: 20px;
  height:20px;
  border: 40px solid #fff;
  background: #000;
  border-radius: 50%;
  position: absolute;
  top:50px;
  left:49%;
}
```

最后推荐一个[网站](https://css-tricks.com/examples/ShapesOfCSS/)第二个方法参考了这个网站。


​    
​    
