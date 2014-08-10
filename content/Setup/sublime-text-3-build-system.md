---
title: "Sublime Text Build System"
layout: page
date: 2014-08-09 00:00
---

# Reference #

[Sublime Text Unofficial Documentation](http://docs.sublimetext.info/en/latest/file_processing/build_systems.html)

## Python ##

Save the following code as `python.sublime-build` in `/Users/lax/Library/Application Support/Sublime Text 3/Packages/User` under Mac OS X

```
{
    "cmd": ["/Users/lax/VEnv/bin/python", "-u", "$file"],
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
    "selector": "source.python"
}
```
