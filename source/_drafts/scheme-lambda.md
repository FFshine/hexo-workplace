---
title: shceme的匿名函数(lambda)
id: 912
categories:
  - 代码
date: 2018-01-18 12:20:04
tags:
---

* * *

在lisp这类元编程中，几乎所有的表达都靠函数，或者是都可以看成是函数。所以在编写lisp时，匿名函数就变得尤其重要。

#### 用法：

**形式一**

<pre>((lambda (形式参数)(表达式))(参数))</pre>

#### 例

<pre>(define (square x)
        ((lambda (x)(* x x))(x)))
(square 5)
> 25
</pre>

**形式二**

<pre>
(lambda(形式参数)(表达式))</pre>

参数在调用时加上。

#### 例2：

<pre>
(define square
   (lamnda (x)(* x x)))
(square 5)
> 25
</pre>