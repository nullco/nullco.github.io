+++
author = "null.co"
title = "Tmux Cheatsheet"
date = "2024-10-24"
description = "Cheatsheet for tmux terminal multiplexer"
tags = [
    "cheatsheet",
    "tmux",
]
categories = [
    "cheatsheet"
]
aliases = ["cheatsheet"]
+++

### Sessions

`tmux ls`  List open sessions

`tmux` Start tmux session (Default name = 0)

`<C-b> d` Detach from session

`tmux attach -t 0` Attach to session with name 0

`tmux new -s session_name` Create session with custom name

`tmux rename-session -t 0 new_name` Rename session

### Panes

`<C-b> %` Vertical split

`<C-b> "` Horizontal split

`<C-d>` Close pane

`<C-b> <arrow>` Move to next pane in direction of `<arrow>`


### Windows

`<C-b> c` Create windows

`<C-b> p` Previous windows

`<C-b> n` Next windows
 
 `<C-b> <number>` Go to window #`<number>`
