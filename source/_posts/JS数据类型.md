---
title: JS数据类型
date: 2018-08-28 15:19:15
tags: JS
---

在JavaScript里使用的每一个值,都属于一种数据类型。也就是因为这些多种的数据类型的支撑才使编程语言更加具有趣味性。  
目前来说JavaScript一共具有七种数据类型 数值(number) ，字符串(string)， 布尔值(boolean)， undefined，null，对象(object)，symbol(ES6新增加的一种数据类型)

- 数值(number)：整数和小数(例如1 1.429 ).
- 字符串(string): 文本('hello world').
- 布尔值(boolean): 表示真假的两个特殊值 true表示真 false表示假.
- undefined：表示未定义或者不存在的,因为目前没有定义,所以不具有任何的值。
- null: 表示空值。说明值存在都是为空。
- 对象(object): 键值对的hash集合。
- symbol:表示一个唯一的值。  

通常我们把数值，字符串，布尔值和symbol称为原始数据类型(primitive type).它们是最基本的数据类型，不能再细分。对象则称为合成类型(complex type).因为一个对象往往是多个原始类型组成的。可以看作存放各种数据的容器。至于undefined 和 null，一般看作两个特殊的类型。  


typeof运算符用来确定这个值是什么类型。

数值，字符串，布尔值和symbol分别返回 number, string, boolean，symbol

```
typeof 3.14 //"number"
typeof "abc" // "string"
typeof true //"boolean"
typeof Symbol('abc') // "symbol"

```
函数返回function 

```
function f() {}
typeof f // "function"
```

null 和 对象返回object

```
var o = {}
typeof o //"object"
typeof null //"object"
```

undefined 

```
a = 'undefined'
typeof a //undefined

```




