---
title: CSS如何实现元素居中
date: 2018-08-07 13:04:37
tags: CSS
---

完整CSS实现的居中的技巧。我只是文章的搬运工完整代码来自[CSS TRICKS](https://css-tricks.com/centering-css-complete-guide/)。  

居中的问题一直都是CSS开发者抱怨的典型问题。为什么它会这么难呢?我认为这种问题不是很难的但是在不同的场合又会出现很多种情况。很难让我们知道如何去解决。接下来让我们通过决策树让它变得简单一点。  
我需要居中...

## - **水平居中**

### 1: 内联元素(文本或者链接)

你可以让内联元素水平居中,通过设置块级父元素text-align: center 代码看下面。  

**html**

```
<body>
    <header>
        This text is centered
    </header>
    <nav class="navigation">
        <a href="#0">One</a>
        <a href="#0">Two</a>
        <a href="#0">Three</a>
        <a href="#0">Four</a>
    </nav>
</body>
```

**css**  

```
body {
    background: #f06d06;
}
          
header, nav {
    text-align: center;
    background: white;
    margin: 20px 0;
    padding: 10px;
}
          
nav a {
    text-decoration: none;
    background: #333;
    border-radius: 5px;
    color: white;
    padding: 3px 8px;
}
```

可以用于 inline inline-block inline-table inline-flex 等等

### 2: 块级元素

让块级元素居中可以给它设置margin-left 和 margin-right属性为auto(如果没有设置宽度它会占据浏览器的宽度也不需要居中)和我经常可以简写类似下面的代码:

**html**

```
<body>
    <main>
        <div class="center">
            I’m a block level element and am centered
        </div>
    </main>
</body>
```

**css**  

```
body {
    background: #f06d06;
}
  
main {
    background: white;
    margin: 20px 0;
    padding: 10px;
}
      
.center {
    margin: 0 auto;
    width: 200px;
    background: black;
    padding: 20px;
    color: white;
}
```

无论你要居中的元素或者父元素的宽度如何都会起作用。  
**注意:你不能设置它们浮动(float)**  

### 3: 多个块级元素

如果你想让两个或者两个以上的块级元素在一行水平居中。你可以设置不同的display属性值。这里有一个设置它们inline-block例子和一个flexbox的例子。  

**html**

```
<body>
    <main class="inline-block-center">
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row.
        </div>
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings do.
        </div>
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row.
        </div>
    </main>
              
    <main class="flex-center">
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row.
        </div>
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings do.
        </div>
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row.
        </div>
    </main>
</body>
```

**css**  

```
body{
    background: #f06d06;
    font-size: 80%;
}

main {
    background: white;
    margin: 20px 0;
    padding: 10px;
}

main div {
    background: black;
    color: white;
    padding: 15px;
    max-width: 125px;
    margin: 5px;
}

.inline-block-center {
    text-align: center;
}

.inline-block-center div {
    display: inline-block;
    text-align: left;
}

.flex-center {
    display: flex;
    justify-content:center;
}
```

如果你希望多个块级元素叠加在一起的这种情况 margin: auto 技术仍然有用。  

**html**

```
<body>
    <main>
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row.
        </div>
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row. I have more content in me than my siblings
            do.
        </div>
        <div>
            I'm an element that is block-like with my siblings and we're centered in a row.
        </div>
    </main>
</body>
```

**css**

```
body {
    background: #f06d06;
    font-size: 80%;
}

main {
    background: white;
    margin: 20px 0;
    padding: 10px;
}

main div {
    background: black;
    margin: 5px auto;
    color: white;
    padding: 15px;
}

main div:nth-child(1) {
    width: 200px;
}

main div:nth-child(2) {

    width: 400px;

}

main div:nth-child(3) {

    width: 125px;
}
```

## 垂直居中

### 1: 内联元素(文本或者链接)

#### 一行垂直居中

有时想让内联元素出现垂直居中,仅仅设置相等的上下padding就可以达到效果。

**html**

```
<body>
    <main>
        <a href="#0">We're</a>
        <a href="#0">Centered</a>
        <a href="#0">Bits of</a>
        <a href="#0">Text</a>
    </main>
</body>
```

**css**

```
body {
    background: #f06d06;
    font-size: 80%;
}
         
main {
    background: white;
    margin: 20px 0;
    padding: 50px;
}

main a {
    background: black;
    color: white;
    padding: 40px 30px;
    text-decoration: none;
}
```

如果不想让padding具有相同的值，而且你又想让文本居中你可以设置notwrap和line-height的数值等于height。 

html

```
<body>
    <main>
        <div>
            I'm a centered line.
        </div>
    </main>
</body>
```

css

```
body {
    background: #f06d06;
    font-size: 80%;
}

main {
    background: white;
    margin: 20px 0;
    padding: 40px;
}

main div {
    background: black;
    color: white;
    height: 100px;
    line-height: 100px;
    padding: 20px;
    width: 50%;
    white-space: nowrap;
}
```

#### 多行垂直居中

设置padding-bottom和padding-top相等对于多行文本也能实现垂直居中的效果。但是如果没有预期的效果,可能是这个元素的文本可能是一个tablecell,无论是这么样,vertical-align属性都可以处理,在这种境况可能不像处理普通的文本一样处理一行的居中。

**html**

```
<table>
    <tr>
        <td>I'm vertically centered multiple lines of text in a real table cell.</td>
    </tr>
</table>
<div class="center-table">
    <p>I'm vertically centered multiple lines of text in a CSS-created table layout.</p>
</div>
```

**css**

```
body{
    background: #f06d06;
    font-size: 80%;
}
table{
    background: white;
    width: 240px;
    border-collapse: separate;
    margin:20px;
    height: 250px;

}
table td {
    background: black;
    color: white;
    padding: 20px;
    border: 10px solid white;
}
.center-table {
    display: table;
    height: 250px;
    background: white;
    width: 240px;
    margin: 20px;
}
.center-table p {
    display: table-cell;
    margin: 0px;
    background: black;
    color: white;
    padding: 20px;
    border: 10px solid white;
    vertical-align: middle;
}
```

你也可以使用flexbox，一个单独的flex-child很简单的可以做到以flex-parent居中。

**html**

```
<body>
    <div class="flex-center">
        <p>I'm vertically centered multiple lines of text in a flexbox container.</p>
    </div>
</body>
```

**css**

```
body{
    background: #f06d06;
    font-size: 80%;
}
div {
    background: white;
    width: 240px;
    margin: 20px;
}
.flex-center {
    background: black;
    color: white;
    border:10px solid white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    height: 200px;
    resize: vertical;
    overflow: auto;
}
.flex-center p {
    margin: 0;
    padding: 20px;
}
```

请记住重要的一点,父容器要具有固定高度（px，％等）也就是包含要居中的元素要有高度。除了这两种技术,您可以使用“ghost元素”技术,将full-height伪元素放置在容器内，文本与该文本垂直对齐。

**html**

```
<div class="ghost-center">
    <p>I'm vertically centered multiple lines of text in a container. Centered with a ghost pseudo element</p>
</div>  
```

**css**

```
 body {
    background: #f06d06;
    font-size: 80%;
}

div {
    background: white;
    width: 240px;
    height: 200px;
    margin: 20px;
    color: white;
    resize: vertical;
    overflow: auto;
    padding: 20px;
}

.ghost-center {
    position: relative;
}
.ghost-center::before {
    content: " ";
    display: inline-block;
    height: 100%;
    width: 1%;
    vertical-align: middle;
}
.ghost-center p {
    display: inline-block;
    vertical-align: middle;
    width: 190px;
    margin: 0;
    padding: 20px;
    background: black;
}
```

### 2：块级元素

#### 元素的高度已知

但如果你知道高度，你可以垂直居中，如：

**html**

```
<body>
    <main>
        <div>
            I'm a block-level element with a fixed height, centered vertically within my parent.
        </div>        
    </main>
</body>
```

**css**

```
 body {
            background: #f06d06;
            font-size: 80%;
        }
        main {
            background: white;
            height: 300px;
            margin: 20px;
            width: 300px;
            position: relative;
            resize: vertical;
            overflow: auto;
        }
        main div {
            position: absolute;
            top: 50%;
            left: 20px;
            right: 20px;
            height: 100px;
            margin-top: -70px;
            background: black;
            color: white;
            padding: 20px;
        }
```

#### 元素的高度未知

已知元素的高度可以

**html**

```
<main>
    <div>
        I'm a block-level element with a fixed height, centered vertically within my parent.
    </div>        
</main>
```

**css**

```
body {
    background: #f06d06;
    font-size: 80%;
}

main {
    background: white;
    height: 300px;
    margin: 20px;
    width: 300px;
    position: relative;
    resize: vertical;
    overflow: auto;
}

main div {
    position: absolute;
    top: 50%;
    left: 20px;
    right: 20px;
    background: black;
    color: white;
    padding: 20px;
    transform: translateY(-50%);
    resize: vertical;
    overflow: auto;
}
```

#### 使用弹性盒(flexbox)

使用flexbox可以非常简单的实现
**
html**

```
<main>
    <div>
        I'm a block-level element with an unknown height, centered vertically within my parent.
    </div>  
</main>
```

**css**

```
body {
  background: #f06d06;
  font-size: 80%;
}

main {
  background: white;
  height: 300px;
  width: 200px;
  padding: 20px;
  margin: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  resize: vertical;
  overflow: auto;
}

main div {
  background: black;
  color: white;
  padding: 20px;
  resize: vertical;
  overflow: auto;
}
```

## - **水平居中并且垂直居中**

### 固定的宽度和高度

使用等于宽度和高度一半的负外边距在相对定位50%处,有跨浏览器作用。

**html**

```
<main>
    <div>
        I'm a block-level element a fixed height and width, centered vertically within my parent.
    </div>    
</main>
```

**css**

```
body {
  background: #f06d06;
  font-size: 80%;
  padding: 20px;
}

main {
  position: relative;
  background: white;
  height: 200px;
  width: 60%;
  margin: 0 auto;
  padding: 20px;
  resize: both;
  overflow: auto;
}

main div {
  background: black;
  color: white;
  width: 200px;
  height: 100px;
  margin: -70px 0 0 -120px;
  position: absolute;
  top: 50%;
  left: 50%;
  padding: 20px;
}
```

### 未知的高度和宽度

如果你不知道高度还有宽度你可以使用trasform属性基于当前的元素的高度和宽度traslate -50%。 

**html**

```
<main>
    <div>
        I'm a block-level element of an unknown height and width, centered vertically within my parent.
    </div>       
</main>
```

**css**

```
body {
  background: #f06d06;
  font-size: 80%;
  padding: 20px;
}

main {
  position: relative;
  background: white;
  height: 200px;
  width: 60%;
  margin: 0 auto;
  padding: 20px;
  resize: both;
  overflow: auto;
}

main div {
  background: black;
  color: white;
  width: 50%;
  transform: translate(-50%, -50%);
  position: absolute;
  top: 50%;
  left: 50%;
  padding: 20px;
  resize: both;
  overflow: auto;
}
```

### 使用弹性盒(flexbox)

**html**

```
<body>
    <main>
        <div>
            I'm a block-level-ish element of an unknown width and height, centered vertically within my parent.
        </div>        
    </main>
</body>
```

**css**

```
body {
  background: #f06d06;
  font-size: 80%;
  padding: 20px;
}

main {
  background: white;
  height: 200px;
  width: 60%;
  margin: 0 auto;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  resize: both;
  overflow: auto;
}

main div {
  background: black;
  color: white;
  width: 50%;
  padding: 20px;
  resize: both;
  overflow: auto;
}
```

### 使用网格(grid)

**html**

```
<span>
    I'm centered!
</span>

```

**css**

```
body, html {
    height: 100%;
    display: grid;
}
span {
 margin: auto;
}


```

















