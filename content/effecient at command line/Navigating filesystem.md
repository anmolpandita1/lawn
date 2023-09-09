---
tags:
  - bash
  - cli
---
[]()
```bash
cd /usr/share/lib/etc/bin              # No matter where you go...
pwd
/usr/share/lib/etc/bin                 # ...there you are.

# navigate to home directory
cd $HOME
cd ~

# The tilde can also refer to another user’s home directory 
# if you place it immediately in front of their username:

# navigate faster using alias
alias work="cd $HOME/Work/Projects/Web/src/include"
work
pwd
/home/smith/Work/Projects/Web/src/include

alias rcedit='$EDITOR $HOME/.bashrc'



# configure $CDPATH
# A cd search path works like your command search path, $PATH, but instead of finding commands, 
# it finds subdirectories. Configure it with the shell variable CDPATH, 
# which has the same format as PATH: a list of directories separated by colons. 
# If your CDPATH consists of these four directories, for example

export CDPATH=$HOME:$HOME/Projects:$HOME/Family/Memories:/usr/local

# then cd will check the existence of the following directories in order, until it finds one or it fails entirely:
# Photos in the current directory
# $HOME/Photos
# $HOME/Projects/Photos
# $HOME/Family/Memories/Photos
# /usr/local/Photos

# The trick is to set up your CDPATH to include, in order:
# $HOME
# Your choice of subdirectories of $HOME
# The relative path for a parent directory, indicated by two dots (..)
# By including $HOME, you can jump immediately to any of its subdirectories 
# (Family, Finances, Linux, Music, and Work) from anywhere else in the filesystem without typing a leading path:

# Place in a shell configuration file and source it:
export CDPATH=$HOME:$HOME/Work:$HOME/Family:$HOME/Linux:$HOME/Music:..

pwd
/usr/src/myproject
ls
docs   include   src

cd docs                              # Change your current directory
cd include
/usr/src/myproject/include           # You jumped to a sibling
cd src
/usr/src/myproject/src               # Again

# if sibling dirs are duplicate, first one is honored 
# duplicate subdirectories check onliner
ls -d */ && (ls -d */*/ | cut -d/ -f2-) | sort | uniq -c | sort -nr | less



# to return to previous directory
# and to toggle between pair of directories use (cd -) repeatedly
cd -



# toggle many directories with pushd and popd
# A directory stack is a list of directories that you’ve visited in the current shell and decided to keep track of.
# You manipulate the stack by performing two operations called pushing and popping.
# Pushing a directory adds it to the beginning of the list, which is traditionally called the top of the stack.
# Popping removes the topmost directory from the stack. Initially, the stack contains only your current directory,
# but you can add (push) and remove (pop) directories and rapidly cd among them.

# clear directory stack
# -c     clear the directory stack.
# -l     print directory names in full instead of using of using ~
#        expressions (see Dynamic and Static named directories in
#        zshexpn(1)).
# -p     print directory entries one per line.
# -v     number the directories in the stack when printing
alias dirs='dirs -v'

Desktop] dirs
0	~/Desktop

Desktop] pushd cheet-sheets
~/Desktop/cheet-sheets ~/Desktop

cheet-sheets] dirs
0	~/Desktop/cheet-sheets
1	~/Desktop

cheet-sheets] popd
~/Desktop

Desktop] dirs
0	~/Desktop
➜  Desktop

# Turn a mistaken cd into a pushd
# Suppose you are jumping among several directories with pushd and you accidentally run cd instead and lose a directory:

$ dirs
~/Work/Projects/Web/src /var/www/html /etc/apache2
$ cd /etc/ssl/certs
$ dirs
/etc/ssl/certs /var/www/html /etc/apache2
# Oops, the accidental cd command replaced ~/Work/Projects/Web/src in the stack with /etc/ssl/certs. 
# But don’t worry. You can add the missing directory back to the stack without typing its long path. 
# Just run pushd twice, once with a dash argument and once without:

$ pushd -
~/Work/Projects/Web/src /etc/ssl/certs /var/www/html /etc/apache2
$ pushd
/etc/ssl/certs ~/Work/Projects/Web/src /var/www/html /etc/apache2

# Let’s dissect why this works:
# The first pushd returns to your shell’s previous directory, ~/Work/Projects/Web/src, and pushes it onto the stack. pushd, like cd, accepts a dash as an argument to mean “go back to my previous directory.”
# The second pushd command swaps the top two directories, bringing you back to /etc/ssl/certs. The end result is that you’ve restored ~/Work/Projects/Web/src to the second position in the stack, exactly where it would have been if you hadn’t made your mistake.
# This “oops, I forgot a pushd” command is useful enough that it’s worth an alias. I call it slurp because in my mind, it “slurps back” a directory that I lost by mistake:

# Place in a shell configuration file and source it:
alias slurp='pushd - && pushd'

# The command pushd (short for “push directory”) does all of the following:
# Adds a given directory to the top of the stack
# Performs a cd to that directory
# Prints the stack from top to bottom for your reference

# The popd command (“pop directory”) is the reverse of pushd. It does all of the following:
# Removes one directory from the top of the stack
# Performs a cd to the new top directory
# Prints the stack from top to bottom for your reference

# shifts N directories from the top of the stack to the bottom and then performs a cd to the new top directory.
pushd +N 
pushd +3 
# A negative argument (-N) shifts directories in the opposite direction, from the bottom to the top, before performing the cd
pushd -N
pushd -3
# To jump to the directory at the bottom of the stack, run pushd -0
pushd -0


dirname  # - containing directory
basename # -  return filename or directory portion of pathname
```