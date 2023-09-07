---
tags:
  - bash
  - cli
---
```bash
# alias and standard commands

alias less="less -c"        # Define an alias
less myfile                 # Run the alias, which invokes less -c
\less myfile                # Run the standard less command, not the alias

source $HOME/.bashrc                 # Uses the builtin "source" command
. $HOME/.bashrc                      # Uses a dot
```