
```bash
#!/bin/bash

# Start a new tmux session named "Testing"
tmux new-session -d -s Testing

# Split the window into two vertical panes
tmux split-window -h

# Attach to the session
tmux attach-session -t Testing

@to swich panes
tmux select-pane -t 1
tmux select-pane -t 0
```

![[Pasted image 20250304145624.png]]