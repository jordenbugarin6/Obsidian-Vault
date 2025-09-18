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