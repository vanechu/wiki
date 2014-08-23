---
title: "Sublime Text Build System"
layout: page
date: 2014-08-09 00:00
---

# Reference #

[Sublime Text Unofficial Documentation](http://docs.sublimetext.info/en/latest/file_processing/build_systems.html)

## Python ##

Save the following code as `*.sublime-build` in `/Users/lax/Library/Application Support/Sublime Text 3/Packages/User` under Mac OS X

```
{
    "cmd": ["/Users/lax/VEnv/bin/python", "-u", "$file"],
    "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
    "selector": "source.python"
}
```

### C++ ###
This configuration is specificed for Clang and assumes Zsh installed.
Save the following code as `*.sublime-build` in `/Users/lax/Library/Application Support/Sublime Text 3/Packages/User` under Mac OS X


```
{
    "cmd": ["clang++", "-std=c++11", "-stdlib=libc++", "${file}", "-o", "${file_base_name}"],
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "working_dir": "${file_path}",
    "selector": "source.c, source.c++",

    "variants":
    [
        {
            "name": "Run",
            "cmd": ["zsh", "-c", "clang++ -std=c++11 -stdlib=libc++ '${file}' -o '${file_path}/${file_base_name}' && '${file_path}/${file_base_name}'"]
        }
    ]
}
```

### User Preferences ###

```
{
    "color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
    "font_face": "Menlo",
    "font_size": 14,
    "theme": "Soda Light 3.sublime-theme",
    "translate_tabs_to_spaces": true,
    "soda_folder_icons": true,
    "ignored_packages":
    [
        "Vintage"
    ]
}
```