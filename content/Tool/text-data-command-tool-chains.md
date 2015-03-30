---
title: "Text Data Command Tool Chains"
layout: page
date: 2014-08-08 00:00
---

# Reference #

[Mac OS X Setup Guide](http://www.sourabhbajaj.com/mac-setup)

## Display the first/last few lines 'head' and 'tail' ##

```
head -n 5 demo.txt
tail -n 5 demo.txt
```

## Display the custom line ##

```
sed -n '9,10p' demo.txt
```


## Create mutiple dictionaries from 001 to 100 ##

```
mkdir {001..100}
```

## Resize Image 

```
ls *.jpg|sed -e 's/\..*//'|xargs -I X convert X.jpg 50% X-resized.jpg

```
