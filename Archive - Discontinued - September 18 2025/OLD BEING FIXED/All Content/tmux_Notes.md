---
created_date: 02 October 2023
updated_date: 15 October 2023
type: linux
"references:": https://www.youtube.com/watch?v=Lqehvpe_djs&t=301s
---
- Tmux is used to allow multiple users to attach to a session
- Used to download/run scripts in background without having to have the terminal open due to running as a process
- changed prefix key to ctrl +a
###### Installing tmux
```bash
sudo apt install tmux
```
###### Tmux config file
```bash
vim ~/.tmux.conf

#Quality of life stuff
set -g history-limit 10000

#tmux logging, takes all terminal information and throws into /opt/tmux-logging/logging.tmux
run-shell /opt/tmux-logging/logging.tmux

command to save tmux-logging:
ctrl b + alt + shift + p
```
###### Creating a new session
```zsh
tmux new-session -s Session1
```
###### Attaching to a new session
```bash
tmux attach-session -t Session1

-t = target session
```
###### Listing existing sessions
```bash
tmux ls
```
###### Create a new window
- press ctrl & b at the same time (prefix key) and then hit c
```bash
ctrl b, c
```
###### Switching windows
```bash
ctrl b, 0
ctrl b, 1
ctrl b, 2
ctrl b, 3
```
###### Vertical splitting terminals
```bash
ctrl b + %
```
###### Horizontal Split
```bash
ctrl b + "
```
###### To move around terminals
```bash
# the terminal with green lines around it is your working directory
ctrl b + <arrow keys>
```
###### To make working terminal full screen - Repeat to zoom out
```bash
ctrl b + z
```
###### To resize terminals
```bash
ctrl b (holding) + <arrow>
```

###### To kill session
```
exit
exit
```
###### Terminal Tricks
```bash
#moves working terminal to left
ctrl b + {
#moves working terminal to right
ctrl b + }
#completely change layout look
ctrl b + spacebar
#cycle through history argument by argument
alt + .
#goes to beginning of line
ctrl + a
# goes to the end of the line
ctrl + e
# goes word by word
ctrl + arrow key
# tmux help screen
ctrl b + ?
# puts timer up
ctrl b + t
```
###
ctrl b , c = making a new window
ctrl b c - create new windows

ctrl b " = splits windows horizontally
ctrl b + = 

tmux new -s main

###### Renaming Session
```bash
ctrl a $
```

###### How to close a pane 
```bash
ctrl a x
```
###### How to crename window
```bash
ctrl a ,
```


conf
```zsh
[root💀~] [192.168.1.155] [2023-11-10 14:45:12] 
 └─╼ # cat ~/.tmux.conf
# This TMUX config requires "xsel" be installed.

#change default /bin/bash shell to /bin/zsh
set-option -g default-shell /bin/zsh

# Change the default $TERM to screen-256color
set -g default-terminal "screen-256color"

# remap prefix from 'C-b' to 'C-a'
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix

# Set scrollback history to 100000 lines
set-option -g history-limit 100000

# Enable vi mode keys by default
setw -g mode-keys vi
set -g mouse on

# turn off auto-renaming
set-window-option -g allow-rename off
set-option -wg automatic-rename off

# DESIGN OPTIONS
# Status Bar options
set-option -g status on
set-option -g status-style bg=colour232,fg=blue
set-window-option -g window-status-style bg=colour231,fg=colour237 

# set -g status-left "#[fg=green] ❐ #S #[default]"

# Set the inactive window color and style
set -g window-status-style fg=colour244,bg=colour237
set -g window-status-format ' [#I] #W '

# Set the active window color and style
set -g window-status-current-style fg=colour233,bg=colour46,bold
set -g window-status-current-format ' [#I] #W '

set -g status-interval 5
set -g status-justify left

# mode style
set -g mode-style fg=colour46,bold,bg=colour233

# message/command bar
set -g message-style fg=colour46,bg=colour233

# Activity Detected stuff
setw -g monitor-activity on
set -g visual-activity off
set-option -gw window-status-activity-style fg=colour46,bg=black,blink

# left status bar
set -g status-left-length 70
set -g status-left "#[fg=white,bold] ❏ #S #[fg=white,bold]  🖥 #(ip addr show  | grep "inet[^6]" | awk '{print $2}')    "

# right status bar
set -g status-right-length 60
set -g status-right "#[fg=white,bold] %A, %B %d %Y - %l:%M %p "

# colors for pane borders
setw -g pane-border-style fg=white,bg=black
setw -g pane-active-border-style fg=colour46,bg=black

# Copy mode bindings (xsel)
bind -T copy-mode    DoubleClick1Pane select-pane \; send -X select-word \; send -X copy-pipe-no-clear "xsel -i"
bind -T copy-mode-vi DoubleClick1Pane select-pane \; send -X select-word \; send -X copy-pipe-no-clear "xsel -i"
bind -n DoubleClick1Pane select-pane \; copy-mode -M \; send -X select-word \; send -X copy-pipe-no-clear "xsel -i"
bind -T copy-mode    TripleClick1Pane select-pane \; send -X select-line \; send -X copy-pipe-no-clear "xsel -i"
bind -T copy-mode-vi TripleClick1Pane select-pane \; send -X select-line \; send -X copy-pipe-no-clear "xsel -i"
bind -n TripleClick1Pane select-pane \; copy-mode -M \; send -X select-line \; send -X copy-pipe-no-clear "xsel -i"
bind -n MouseDown2Pane run "tmux set-buffer -b primary_selection \"$(xsel -o)\"; tmux paste-buffer -b primary_selection; tmux delete-buffer -b primary_selection"

# Initialize TPM
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'
set -g @plugin 'tmux-plugins/tmux-yank'

# Future integration of continuous tmux env saves; further testing needed
#set -g @plugin 'tmux-plugins/tmux-resurrect'
#set -g @plugin 'tmux-plugins/tmux-continuum'
#set -g @continuum-restore 'on'

set -g @yank_action 'copy-pipe-no-clear'
bind -T copy-mode    C-c send -X copy-pipe-no-clear "xsel -i --clipboard"
bind -T copy-mode-vi C-c send -X copy-pipe-no-clear "xsel -i --clipboard"

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'

```

┌──(root💀gobots)-[10Nov2023 15:04:37]-[~]
└─# hello

to copy and paste shift for regular functionality
```
```