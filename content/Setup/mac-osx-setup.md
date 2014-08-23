---
title: "Mac OS X Setup"
layout: page
date: 2014-08-08 00:00
---

# Reference #

[Mac OS X Setup Guide](http://www.sourabhbajaj.com/mac-setup)

### Alias

OS X has a neat command-line tool called pbcopy which takes the standard input and places it in the clipboard to paste into other applications.

In Ubuntu(or any Linux distro with Xwindows), a similar tool is xclip.

```
alias pbcopy='xclip -selection clipboard'
alias pbpaste='xclip -selection clipboard -o'
```
Now you can pipe any text to pbcopy

```
cat ~/.ssh/id_dsa.pub | pbcopy
```

## Python ##
I highly recommend to use Anaconda.

Test openblas and such kind of things.

```
python -c "import numpy as np; np.show_config()"
```
Install openblas then compiling numpy 

http://dedupe.readthedocs.org/en/latest/OSX-Install-Notes.html


## C++ ##
Make sure you have installed Xcode command line tools. Check the c++ version to make sure it is Clang 4.0+

```
$ c++ --version
Apple LLVM version 5.1 (clang-503.0.38) (based on LLVM 3.4svn)
Target: x86_64-apple-darwin13.1.0
Thread model: posix
```

Then create an alias for c++11 installation in your env.sh file.

```
alias cppcompile='c++ -std=c++11 -stdlib=libc++'
```

Then you can run all cpp file directly using `cppcompile main.cpp` and it will use c++11 so no errors in the case of using vectors, auto, sets etc.

## Java ##
Check if Java is already installed

```
$ java -version
```

If you see an output like below then Java is already installed on your machine so skip the next step.

```
java version "1.8.0_05"
Java(TM) SE Runtime Environment (build 1.8.0_05-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.5-b02, mixed mode)
```

If you don't see the output like above then you need to install Java on your system. Please download the OS X version from the [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/).

Check if Java is correctly installed by running the `java -version` command again.

Add `JAVA_HOME` to your environment variables by adding the line below to your `env.sh`.

```
export JAVA_HOME="`/usr/libexec/java_home -v 1.8`"
```

You should have JAVA working now. If you use Eclipse as your Java IDE it'll prompt you to install Java 6, go ahead and click Ok.