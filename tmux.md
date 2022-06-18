# tmux Quickstart
- https://en.wikipedia.org/wiki/Tmux
- https://www.howtogeek.com/671422/how-to-use-tmux-on-linux-and-why-its-better-than-screen/

## Panes
- `Ctrl` + `b`, `"`: split pane in half horizontally
- `Ctrl` + `b`, `%`: split pane in half veritically
- `Ctrl` + `b`, `o`: go to next pane
- `Ctrl` + `b`, Arrow: go to pane
- `Ctrl` + `b`, `x`: kill pane
- `Ctrl` + `b`, `z`: toggle pane zoom mode (full screen)

## Windows
- `Ctrl` + `b`, `c`: create new window
- `Ctrl` + `b`, NumberX : switch to window #NumberX
- `Ctrl` + `b`, `,`: name window

## General
- `Ctrl` + `b`, `$`: rename session
- `Ctrl` + `b`, `d`: detach session
- `tmux ls`: list all sessions
- `tmux attach -t numberOrNameInList`: reattach session
- `Ctrl` + `:`: Command mode (to enter 
- `set-option -g mouse on` [in config (`$HOME/.tmux.conf`) or in Command mode]: Allow mouse scrolling  # https://superuser.com/a/1211928
