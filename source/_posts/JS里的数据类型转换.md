---
title: JS里的数据类型转换
date: 2018-08-31 05:20:47
tags: JS
---

1. 数值型(Number)

- 转字符串
```
var a = 100
a.toString() //"100"
String(a) //"100"
a + '' // "100"
```
- 转布尔型

```
Boolean(1) // true
Boolean(0) // false
Boolean(NaN) // false

!!1 //true
!!0 // false
!!NaN //false
```

- 转对象型

```
new Number(1)
```


2. 字符串(String)

- 转布尔型

```
Boolean('purcy') //true
Boolean('') //false

!!"purcy" // true
!!'' // false
```

- 转数值型

```
Number('11') //11
Number('0x11') //17
Number('0b11')//3
Number('0o11')//9
Number(' ')//0
Number('')//0
Number('abc')// NaN
Number(' 11')//11
Number('11a')//NaN
Number('1.34') //1.34
Number('NaN')//NaN
Number('Infinity')//Infinity
Number('-Infinity')//-Infinity
Number('1e3') // 1000

parseInt('11')//11
parseInt('0x11')//17
parseInt('0b11')//3
parseInt('0o11')//9
parseInt(' ')//NaN
parseInt('')//NaN
parseInt('abc')//11
parseInt('11a')//11
parseInt('Infinity') //NaN
parseInt('1e3') //1

//Number()可以转换所有是数值型的字符串如果碰到不能转化的为NaN
//parseInt parseFloat  如果碰到不是数值的字符串立即停止转换并把之前转换的值输出如果第一个值不能转化直接为NaN


+"11" //11
+'12.3' //12.3
+'1E3' //1000
+'11a' //

//用运算符 + 也可以达到与Number() 相同的效果
```


- 转对象型

```
new String('purcy')
```

3. 布尔型(Boolean)  

- 转字符串

```
var a = true
a.toString() //"true"
String(a) //"true"
a + "" // "true"
```

- 转数值型

```
Number(true)  //1
Number(false) //0

parseInt(true) //NaN
parseInt(false) //NaN
```


- 转对象型

```
new Boolean(true)
```

4. null  

-  转字符串


```
String(null) // "null"
null + '' // "null"
```

- 转布尔型

```
Boolean(null) // false
!!null //false
```

- 转数值型

```
Number(null) // 0

parseInt(null) //NaN
```

5. undefined  

-  转字符串

```
String(undefined) // "undefined"
undefined + '' // "undefined"
```

- 转布尔型

```
Boolean(undefined) //false
!!undefined //false
```

- 转数值型

```
Number(undefined) // NaN

parseInt(undefined) //NaN
```

6. 对象型(Object)

-  转字符串

```
var obj = {name: 'purcy'}
obj.toString() //"[Object Object]"
obj+ '' // "[Object Object]"
JSON.stringify(obj) // "{"name":"purcy"}"

```

- 转布尔型

```
var obj = {name: 'purcy'}
Boolean(obj) //true
Boolean({}) //true
!!obj //true
!!{} //true
```

- 转数值型

```
//所有对象转为数值都为NaN
```