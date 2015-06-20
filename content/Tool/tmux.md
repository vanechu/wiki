---
title: "Tmux"
layout: page
date: 2015-06-20 00:00
---

# Reference #

[Linux下终端利器tmux](http://kumu-linux.github.io/blog/2013/08/06/tmux/)

## Notion

tmux contains:

- session :一个服务器可以包含多个会话
- window :一个会话可以包含多个窗口
- pane :一个窗口可以包含多个面板[强悍的分屏]

## Usage

`Ctrl+b` first, then: 


### Basic

```
?     列出所有快捷键；按q返回
d     脱离当前会话,可暂时返回Shell界面，输入tmux attach能够重新进入之前会话
s     选择并切换会话；在同时开启了多个会话时使用
D     选择要脱离的会话；在同时开启了多个会话时使用
:     进入命令行模式；此时可输入支持的命令，例如kill-server所有tmux会话
[     复制模式，光标移动到复制内容位置，空格键开始，方向键选择复制，回车确认，q/Esc退出
]     进入粘贴模式，粘贴之前复制的内容，按q/Esc退出
~     列出提示信息缓存；其中包含了之前tmux返回的各种提示信息
t     显示当前的时间
Ctrl+z  挂起当前会话
```

### Window keys

```
c     创建新窗口
&     关闭当前窗口
Number     切换到指定窗口
p     切换至上一窗口
n     切换至下一窗口
l     前后窗口间互相切换
w     通过窗口列表切换窗口
,     重命名当前窗口，便于识别
.     修改当前窗口编号，相当于重新排序
f     在所有窗口中查找关键词，便于窗口多了切换
```

### Panel keys

```
"           将当前面板上下分屏
%           将当前面板左右分屏
x           关闭当前分屏
!           将当前面板置于新窗口,即新建一个窗口,其中仅包含当前面板
Ctrl+Arrow  以1个单元格为单位移动边缘以调整当前面板大小
Alt+Arrow   以5个单元格为单位移动边缘以调整当前面板大小
Space       可以在默认面板布局中切换，试试就知道了
q           显示面板编号
o           选择当前窗口中下一个面板
Arrow       移动光标选择对应面板
{           向前置换当前面板
}           向后置换当前面板
Alt+o       逆时针旋转当前窗口的面板
Ctrl+o      顺时针旋转当前窗口的面板
z           tmux 1.8新特性，最大化当前所在面板
```

## .tmux.conf

`kumu's` config

```
# Set prefix key to Ctrl-a
unbind-key C-b
set-option -g prefix C-a
bind-key C-a last-window # 方便切换，个人习惯
bind-key a send-prefix
# shell下的Ctrl+a切换到行首在此配置下失效，此处设置之后Ctrl+a再按a即可切换至shell行首

# reload settings # 重新读取加载配置文件
bind R source-file ~/.tmux.conf \; display-message "Config reloaded..."

# Ctrl-Left/Right cycles thru windows (no prefix) 
# 不使用prefix键，使用Ctrl和左右方向键方便切换窗口
bind-key -n "C-Left" select-window -t :-
bind-key -n "C-Right" select-window -t :+

# displays 
bind-key * list-clients

set -g default-terminal "screen-256color"   # use 256 colors
set -g display-time 5000                    # status line messages display
set -g status-utf8 on                       # enable utf-8 
set -g history-limit 100000                 # scrollback buffer n lines
setw -g mode-keys vi                        # use vi mode

# start window indexing at one instead of zero 使窗口从1开始，默认从0开始 
set -g base-index 1

# key bindings for horizontal and vertical panes
unbind %
bind | split-window -h      # 使用|竖屏，方便分屏
unbind '"'
bind - split-window -v      # 使用-横屏，方便分屏

# window title string (uses statusbar variables)
set -g set-titles-string '#T'

# status bar with load and time 
set -g status-bg blue
set -g status-fg '#bbbbbb'
set -g status-left-fg green
set -g status-left-bg blue
set -g status-right-fg green
set -g status-right-bg blue
set -g status-left-length 90
set -g status-right-length 90
set -g status-left '[#(whoami)]'
set -g status-right '[#(date +" %m-%d %H:%M ")]'
set -g status-justify "centre"
set -g window-status-format '#I #W'
set -g window-status-current-format ' #I #W '
setw -g window-status-current-bg blue
setw -g window-status-current-fg green

# pane border colors
set -g pane-active-border-fg '#55ff55'
set -g pane-border-fg '#555555'
```


## Launch with script

```
tmux_init()
{
    tmux new-session -s "kumu" -d -n "local"    # 开启一个会话
    tmux new-window -n "other"          # 开启一个窗口
    tmux split-window -h                # 开启一个竖屏
    tmux split-window -v "top"          # 开启一个横屏,并执行top命令
    tmux -2 attach-session -d           # tmux -2强制启用256color，连接已开启的tmux
}

# 判断是否已有开启的tmux会话，没有则开启
if which tmux 2>&1 >/dev/null; then
    test -z "$TMUX" && (tmux attach || tmux_init)
fi
```


