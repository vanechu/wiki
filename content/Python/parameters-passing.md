---
title: "Parameter passing"
layout: page
date: 2014-08-17 00:00
---

# Reference #

[python函数的四种参数传递方式](http://freshstu.com/2013/04/four-kinds-of-function-argment-pass-in-python/)



There are four types to pass parameters.

## `fun1(a,b,c)` ##


## `fun2(a=1,b=2,c=3)` ##


## `fun3(*args)` ##


## `fun4(**kargs)` ##



```
def test(x,y=5,*,**b):
   print x,y,a,b

test(1) ===> 1 5 () {}
test(1,2) ===> 1 2 () {}
test(1,2,3) ===> 1 2 (3,) {}
test(1,2,3,4) ===> 1 2 (3,4)
test(x=1) ===> 1 5 () {}
test(x=1,y=1) ===> 1 1 () {}
test(x=1,y=1,a=1) ===> 1 1 () {'a':1} test(x=1,y=1,a=1,b=1) ===> 1 1 () {'a':1,'b':1}
test(1,y=1) ===> 1 1 () {}
test(1,2,y=1) ===> error, assign multiple values to 'y'
test(1,2,3,4,a=1) ===> 1 2 (3,4) {'a':1}
test(1,2,3,4,k=1,t=2,o=3) ===> 1 2 (3,4) {'k':1,'t':2,'o':3}

```
