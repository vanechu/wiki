---
title: "Editor Shortcuts"
layout: page
date: 2015-06-21 00:00
---


## GNU Readline

### Basic moves
```
Move back one character.        Ctrl + b
Move forward one character.     Ctrl + f
Delete current character.       Ctrl + d
Delete previous character.      Backspace
Undo.                           Ctrl + -
```

### Moving faster
```
Move to the start of line.      Ctrl + a
Move to the end of line.        Ctrl + e
Move forward a word.            Meta + f (a word contains alphabets and digits, no symbols)
Move backward a word.           Meta + b
Clear the screen.               Ctrl + l
```

What is `Meta`? `Meta` is your `Alt` key, normally. For Mac OSX user, you need to enable it yourself. Open Terminal > Preferences > Settings > Keyboard, and enable Use option as meta key. Meta key, by convention, is used for operations on word.

### Cut and paste

```
Cut from cursor to the end of line.       Ctrl + k
Cut from cursor to the end of word.       Meta + d
Cut from cursor to the start of word.     Meta + Backspace
Cut from cursor to previous whitespace.   Ctrl + w
Paste the last cut text.                  Ctrl + y
Loop through and paste previously cut text. Meta + y (use it after Ctrl + y)
Loop through and paste the last argument of previous commands. Meta + .
```

### Search the command history

```
Search as you type. Ctrl + r and type the search term; Repeat Ctrl + r to loop through results.
Search the last remembered search term. Ctrl + r twice.
End the search at current history entry. Ctrl + j
Cancel the search and restore original line. Ctrl + g
```

### Reference

[Bash Reference Manual](http://www.gnu.org/software/bash/manual/bashref.html#Command-Line-Editing)
[Shortcuts to Move Faster in Bash Command Line](http://teohm.com/blog/2012/01/04/shortcuts-to-move-faster-in-bash-command-line/)


## Sublime Text 3

### Editing

| Keypress      | Command                                                                   |
|-------------- |-------------------------------------------------------------------------- |
| Ctrl + X      | Cut line                                                                  |
| Ctrl + ↩      | Insert line after                                                         |
| Ctrl + ⇧ + ↩  | Insert line before                                                        |
| Ctrl + ⇧ + ↑  | Move line/selection up                                                    |
| Ctrl + ⇧ + ↓  | Move line/selection down                                                  |
| Ctrl + L      | Select line - Repeat to select next lines                                 |
| Ctrl + D      | Select word - Repeat select others occurrences                            |
| Ctrl + M      | Jump to closing parentheses Repeat to jump to opening parentheses         |
| Ctrl + ⇧ + M  | Select all contents of the current parentheses                            |
| Ctrl + ⇧ + K  | Delete Line                                                               |
| Ctrl + KK     | Delete from cursor to end of line                                         |
| Ctrl + K + ⌫  | Delete from cursor to start of line                                       |
| Ctrl + ]      | Indent current line(s)                                                    |
| Ctrl + [      | Un-indent current line(s)                                                 |
| Ctrl + ⇧ + D  | Duplicate line(s)                                                         |
| Ctrl + J      | Join line below to the end of the current line                            |
| Ctrl + /      | Comment/un-comment current line                                           |
| Ctrl + ⇧ + /  | Block comment current selection                                           |
| Ctrl + Y      | Redo, or repeat last keyboard shortcut command                            |
| Ctrl + ⇧ + V  | Paste and indent correctly                                                |
| Ctrl + Space  | Select next auto-complete suggestion                                      |
| Ctrl + U      | soft undo; jumps to your last change before undoing change when repeated  |
| Alt + ⇧ + W   | Wrap Selection in html tag                                                |

### Linux

| Keypress        | Command                 |
|---------------- |-----------------------  |
| Alt + ⇧ + Up    | Column selection up     |
| Alt + ⇧ + Down  | Column selection down   |

### Navigation/Goto Anywhere

| Keypress  | Command                     |
|---------- |---------------------------  |
| HOME      | Move to begining of line    |
| END       | Move to ending of line      |
| Ctrl + P  | Quick-open files by name    |
| Ctrl + R  | Goto symbol                 |
| Ctrl + ;  | Goto word in current file   |
| Ctrl + G  | Goto line in current file   |

### General

| Keypress            | Command                   |
|-------------------- |-------------------------- |
| Ctrl + ⇧ + P        | Command prompt            |
| Ctrl + KB           | Toggle side bar           |
| Ctrl + ⇧ + Alt + P  | Show scope in status bar  |

### Find/Replace

| Keypress      | Command         |
|-------------- |---------------  |
| Ctrl + F      | Find            |
| Ctrl + H      | Replace         |
| Ctrl + ⇧ + F  | Find in files   |

### Tabs

| Keypress      | Command                                                   |
|-------------- |---------------------------------------------------------- |
| Ctrl + ⇧ + t  | Open last closed tab                                      |
| Ctrl + PgUp   | Cycle up through tabs                                     |
| Ctrl + PgDn   | Cycle down through tabs                                   |
| Ctrl + ⇆      | Find in files                                             |
| Ctrl + W      | Close current tab                                         |
| Alt + [NUM]   | Switch to tab number [NUM] where [NUM] <= number of tabs  |

### Split window

| Keypress          | Command                                         |
|------------------ |-----------------------------------------------  |
| Alt + ⇧ + 2       | Split view into two columns                     |
| Alt + ⇧ + 1       | Revert view to single column                    |
| Alt + ⇧ + 5       | Set view to grid (4 groups)                     |
| Ctrl + [NUM]      | Jump to group where num is 1-4                  |
| Ctrl + ⇧ + [NUM]  | Move file to specified group where num is 1-4   |

### Bookmarks

| Keypress        | Command             |
|---------------  |-------------------  |
| Ctrl + F2       | Toggle bookmark     |
| F2              | Next bookmark       |
| ⇧ + F2          | Previous bookmark   |
| Ctrl + ⇧ + F2   | Clear bookmarks     |

### Text manipulation

| Keypress    | Command                 |
|-----------  |------------------------ |
| Ctrl + KU   | Transform to Uppercase  |
| Ctrl + KL   | Transform to Lowercase  |







