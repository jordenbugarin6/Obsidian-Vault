```bash
#ignore everything going to type
export HISTIGNORE='*'
```

```bash
# Turn history back on
set -o history

# Reset HISTFILE back to default
export HISTFILE=~/.bash_history
unset HISTIGNORE
```