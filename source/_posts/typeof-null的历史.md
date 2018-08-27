---
title: typeof null的历史
date: 2018-08-27 19:51:48
tags:JS
---

 在javaScript, =='typeof null is object'== 于是让一些人误认为*null*是一个对象(null不是对象,它是一个原生类型)。这是一个bug而且很不辛运的是不能被修复。因为这 样会打破先存在的代码。下面让我们探索bug的历史吧。   
 =='typeof null'== 这个bug在js第一个版本已经遗留下来了。在这个版本值以32位的形式被存储。它们由类型标签(1-3bit)和真实的数据值组成。类型标签在低位被存储。下面是5种数据类型的类型标签的形式。

-  000: object。这些数据代表着对象。
-  1：int 这些数据是31位的有符号整数
-  010：double。这些数据代表着双精度浮点型数值
-  100：string 这些数据代表的着字符串。
-  110：boolean。这些数据代表着布尔值。  

两个特殊:  

    undefined(JSVAL_VOID)数值为integer -2^30 
    null(JSVAL_NULL)是机器码的NULL指针.并且 对象类型的标签也被当作为0.
 这也就显而易见的为什么typeof的null是对象了。下面是typeof的JS引擎源码

```
JS_PUBLIC_API(JSType)
    JS_TypeOfValue(JSContext *cx, jsval v)
    {
        JSType type = JSTYPE_VOID;
        JSObject *obj;
        JSObjectOps *ops;
        JSClass *clasp;

        CHECK_REQUEST(cx);
        if (JSVAL_IS_VOID(v)) {  // (1)
            type = JSTYPE_VOID;
        } else if (JSVAL_IS_OBJECT(v)) {  // (2)
            obj = JSVAL_TO_OBJECT(v);
            if (obj &&
                (ops = obj->map->ops,
                 ops == &js_ObjectOps
                 ? (clasp = OBJ_GET_CLASS(cx, obj),
                    clasp->call || clasp == &js_FunctionClass) // (3,4)
                 : ops->call != 0)) {  // (3)
                type = JSTYPE_FUNCTION;
            } else {
                type = JSTYPE_OBJECT;
            }
        } else if (JSVAL_IS_NUMBER(v)) {
            type = JSTYPE_NUMBER;
        } else if (JSVAL_IS_STRING(v)) {
            type = JSTYPE_STRING;
        } else if (JSVAL_IS_BOOLEAN(v)) {
            type = JSTYPE_BOOLEAN;
        }
        return type;
    }
```

在(1)引擎文件检测v是否为undefined(VOID).这个检查执行了值得比较。

```
#define JSVAL_IS_VOID(v)  ((v) == JSVAL_VOID)
```
在(2)检测value是否为对象的标签。如果条件符合调用(3)或者它被内部的属性[[Class]]标记它为是function.所以这个v是个函数。否者他是个对象。这也由typeof null生成的结果。
随后检查数值 字符串 布尔。甚至没有显示的检查null。这可以由以下的C的宏执行。

```
  #define JSVAL_IS_NULL(v)  ((v) == JSVAL_NULL)
```

这些都是看起来很显而易见的bug。不要忘记了javaScript在极短的时间被完成了第一个版本。





  



   

 

 
