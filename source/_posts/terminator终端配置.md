---
title: terminator终端配置
tags:
  - 教程
  - linux
categories: 教程
copyright: true
description: terminator终端配置，修改终端大小和起始位置
abbrlink: a8de52a9
date: 2023-04-12 19:52:50
update: 2023-04-12 19:52:50
---

## 安装terminator

    sudo apt-get install terminator

## 美化terminator

- 新建配置文件

      mkdir ~/.config/termintor && gedit ~/.config/terminator/config


- 复制以下配置文件


        [global_config]
          focus = system
          title_transmit_bg_color = "#3e3838"
          suppress_multiple_term_dialog = True
        [keybindings]
          split_vert = <Shift><Alt>o
        [profiles]
          [[default]]
            background_color = "#002b36"
            background_darkness = 0.85
            cursor_color = "#e8e8e8"
            font = Ubuntu Mono 14
            foreground_color = "#e8e8e8"
            show_titlebar = False
            palette = "#2d2d2d:#f2777a:#99cc99:#ffcc66:#6699cc:#cc99cc:#66cccc:#d3d0c8:#747369:#f2777a:#99cc99:#ffcc66:#6699cc:#cc99cc:#66cccc:#f2f0ec"
            use_system_font = False
            copy_on_selection = True
        [layouts]
          [[default]]
            [[[child1]]]
              type = Terminal
              parent = window0
              profile = default
            [[[window0]]]
              type = Window
              parent = ""
              size = 900, 600
              position = 1000:500
        [plugins]


    如果你需要修改terminal的大小和起始位置，只需要修改size和position的值。这里设置的位置是4K显示器中间位置。