---
title: CSS布局的那些事
date: 2018-08-08 00:03:33
tags: CSS
---

页面布局是web前端的重要的知识点。当我们写页面最开始考虑的就是页面布局。下面由一道面试题说一说CSS页面布局的那些事。

**题目: 高度已知,请写出三栏布局, 其中左栏 右栏宽度各为300px,中间自适应？**

**1: 浮动布局(float)**  

**优点：**  兼容性比较好,几乎可以适配现代的所有浏览器。

**缺点：** 浮动会脱离文档流 需要清除浮动 处理周边元素的关系。

**html** 

```
<section class="float">
   <article class="container clearfix">
        <div class="left"></div>
         <div class="center">
            <h1>浮动布局</h1>
        </div>
        <div class="right"></div>
   </article>
</section>
```
**css**

```
section.float>.container>div{
    min-height: 300px;
}

section.float>.container>.left{
    float: left;
    width: 300px;
    background: red;
}

section.float>.container>.right{
    float: right;
    width: 300px;
    background: blue;
}

section.float>.container>.center{
    background: yellow;
}

section.float>.container>.center>h1{
   text-align: center;
}

.clearfix::after{
    content: "";
    display: block;
    clear: both;
}
```

---

**2: 绝对定位(position: absolute)**  

**优点：** 简单 快捷。 

**缺点：** 布局脱离文档流也意味着子元素也要脱离文档流导致可使用性比较差。

**html** 

```
<section class="absolute">
   <article class="container">
        <div class="left"></div>
        <div class="center">
            <h1>绝对定位</h1>
        </div>
        <div class="right"></div>
   </article>
</section>
```
**css**

```
section.absolute>.container>div{
    min-height: 300px;
    position: absolute;
}

section.absolute>.container>.left{
    left: 0px;
    width: 300px;
    background: red;
}

section.absolute>.container>.right{
    right: 0px;
    width: 300px;
    background: blue;
}

section.absolute>.container>.center{
    left: 300px;
    right: 300px;
    background: yellow;
}

section.absolute>.container>.center>h1{
   text-align: center;
}
```

---

**3: 弹性盒布局(flexbox)**

**优点**：flexbox是为了解决上面两种问题出现的新解决方案解决移动端布局问题。 

**缺点：** 对于一些老的浏览器不兼容。

**html**

```
<section class="flexbox">
    <article class="container">
        <div class="left"></div>
        <div class="center">
            <h1>弹性盒布局</h1>
        </div>
        <div class="right"></div>
    </article>
</section>
```
**css**

```
section.flexbox>.container {
    display: flex;
}

section.flexbox>.container>div {
    min-height: 300px;
}

section.flexbox>.container>.left {

    width: 300px;
    background: red;
}

section.flexbox>.container>.right {

    width: 300px;
    background: blue;
}

section.flexbox.container>.center {
    flex: 1;
    background: yellow;
}

section.flexbox>.container>.center>h1 {
    text-align: center;
}
```

---

**4: 表格布局(display: table)**  

**优点：** 兼容性比较好在考虑flex布局兼容性的问题表格布局最佳选择。

**缺点：**  对seo不友好 复杂 繁琐。 

**html**

```
<section class="table">
   <article class="container">
        <div class="left"></div>
        <div class="center">
            <h1>表格布局</h1>
        </div>
        <div class="right"></div>
   </article>
</section>
```
**css**

```
section.table>.container{
    display: table;
    width: 100%;
    height: 300px;
}

section.table>.container>div{
   display: table-cell;
}

section.table>.container>.left{
 
    width: 300px;
    background: red;
}

section.table>.container>.right{
   
    width: 300px;
    background: blue;
}

section.table>.container>.center{
    background: yellow;
}

section.table>.container>.center>h1{
   text-align: center;
}
```

---

**5: 网格布局(grid)**

**优点：** 比较完美的解决方案。

**缺点：** 兼容性比较差 复杂。

**html**

```
<section class="grid">
   <article class="container">
        <div class="left"></div>
        <div class="center">
            <h1>网格布局</h1>
        </div>
        <div class="right"></div>
   </article>
</section>
```
**css**

```
section.grid>.container{
    display: grid;
    width: 100%;
    grid-template-rows: 300px;
    grid-template-columns: 300px auto 300px;
}
section.grid>.container>.left{
    background: red;
}
section.grid>.container>.right{
    background: blue;
}
section.grid>.container>.center{
    background: yellow;
}
section.grid>.container>.center>h1{
   text-align: center;
}
```

---

更多关于页面布局请点击[这里](https://css-tricks.com/guides/layout/)。