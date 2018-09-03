---
title: JS原型链和继承
date: 2018-09-03 17:35:42
tags: JS
---

在下面的两部分文章我会用自己的想法来解释JavaScript的原型链和继承。

**JavaScript一个被鄙视的编程语言**  
可以说JavaScript是最被鄙视的编程语言之一。然而，它也是最被欢迎的编程语言之一，而且我每天会以2各种形式遇见他。

大部分人的迷惑可能来至两个部分的迷惑: 原形链和作用域。  
JavaScript有着和大部分其他编程语言不同的继承方式和作用域。我想能正确的理解你就可以了解到这些的潜力。

**JavaScript的原形链**  
JS有着完全不同于大部分面向对象语言有趣的继承模型。它实现面向对象的方式不是通过类而是通过方法。这是一个很重要概念去理解JS的面向对象。

**JavaScript的构造器**  
创建一个对象在JavaScript首先你必须定义一个构造函数。

```
var LivingEntity = function(location) {
   this.x = location.x;
   this.y = location.y;
   this.z = location.z;
}
//创建一个新的实例
var dog = new LivingEntity({
    x: 5,
    y：0，
    z: 1
});
```
这个构造函数不在是普通的函数。你可能注意到this的引用,this对于构造函数不是特殊的而且你可以在任何的函数内部去引用到它。通常这是重要的一点在执行函数的作用域中。

创建一个对象的实例,我们需要用new关键字去调用构造函数。

**方法**  
来让我们看看如何添加一个方法吧。我们把声明的方法加moveWest。方法的功能让x的数值减一。

```
//在构造函数内部
var LivingEntity = function(location){
	this.x = location.x;
	this.y = location.y;
	this.z = location.z;
	this.moveWest = function(){
		this.x--;
	}
};

//在构造函数之后
dog.moveWest = function(){
	this.x--;
}
```
这样做不是使用原型构造对象的方法，并且这两种方法都会向内存中添加不必要的匿名函数。

相反，我们可以在原型链中添加一个匿名函数！

```
LivingEntity.prototype.moveWest = function(){
	this.x--;
}
```

如果我们这样做，只有一个匿名函数，其引用传递给所有LivingEntity对象。

但什么是<Function> .prototype？ prototype是所有函数的一个属性，并指向一个对象，在该对象中可以分配属性，该属性能够从使用该函数创建的所有对象作为构造函数进行访问。

每个对象都有prototype。我们可以修改它甚至是Object。

```
Object.prototype.a = 5;

var v = {};
console.log(v.a); //5
```
对象的原型是一种在类的所有实例中存储公共属性的方法，但是以可重写的方式存储。 如果对象没有对属性的引用，则将检查该对象的原型以查找该属性。

```
LivingEntity.prototype.makeSound = function(){
	console.log('meow');
}

//原型链上的
dog.makeSound(); //meow

dog.makeSound = function(){
	console.log('woof');
}

//自己本身的
dog.makeSound(); //woof
```
**原形链**  
每个对象都有一个原型，包括原型对象。 这个“链”一直向前，直到它到达一个没有原型的对象，通常是Object的原型。 Prototype的“继承”版本涉及在该原型链的末尾添加另一个链接，如下所示。


```
var Dragon = function(location){  
    
    //继承LivingEntity所有属性。
    LivingEntity.call(this, location);
    //增加自己的属性。
    this.canFly = true;
};

//继承LivingEntity原形链上的方法
Dragon.prototype = Object.create(LivingEntity.prototype);

//指向正确的构造函数。
Dragon.prototype.constructor = Dragon;

Dragon.prototype.fly = function(y){  
    this.y += y;
}

var sparky = new Dragon({  
    x: 0,
    y: 0,
    z: 0
});  
```
在对象上调用属性时，首先检查该对象是否存在该属性，如果该属性不存在，则遍历其原型链中的每个链接，直到找到该属性或到达该结尾。 通过这种方式，即使moveWest没有在其直接原型中定义，sparky也可以使用moveWest。

什么是sparky及其原型链看起来只有列出每个对象的特定属性？

- sparky   
   x   
    y   
    z   
   canFly   
- sparky.prototype (Dragon.prototype)   
  fly  
- sparky.prototype.prototype   (LivingEntity.prototype)  
  makeSound  
  moveWest  
- sparky.prototype.prototype.prototype   (Object.prototype)   
  create   
  toString  
  etc...  