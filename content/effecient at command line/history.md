---
tags:
  - bash
  - cli
---

```bash
history
 1000  cd $HOME/Music
 1001  ls
 1002  mv jazz.mp3 jazzy-song.mp3
 1003  play jazzy-song.mp3
 ⋮                                      # Omitting 477 lines
 1481  cd

history 3                               # Print the 3 most recent commands
 1482  firefox https://google.com
 1483  history
 1484  history 3

history | less                      # Earliest to latest entry
history | sort -nr | less           # Latest to earliest entry

history | grep -w cd
 1000  cd $HOME/Music
 1092  cd ..


# delete history for current shell
history -c    

# history size
HISTSIZE=10000
#history ignore duplicates
HISTCONTROL=ignoredups
# history file, where history is stored
echo $HISTFILE
# history file size in lines
echo $HISTFILESIZE

# prev command
!! 

# most recent usage of command
# grep in this case
!grep

# To refer to the most recent command that contained a given string somewhere, 
# not just at the beginning of the command, surround the string with question marks as well
!?grep?
history | grep -w cd
 1000  cd $HOME/Music
 1092  cd ..

# run the command at position 1023 in the history
!1000
cd $HOME/Music

# the command you executed three commands ago
!-3 
rm *

# print not executed (blindly executing can be dangerous)
# but appended to history
# follow by running !!
# no need to select and paste
!-3:p 
rm * 

# final word/argument of most recent command
cat file.txt
echo !$
file.txt

# all words/arguments of most recent command
cat file.txt file2.txt
echo !*
file.txt file2.txt

# INCREMENTAL SEARCH
Ctrl + R, followed by ENTER
# recall most recent string you searched for:
(Ctrl + R) * 2 time 


# EDITING MISTAKES
# Suppose you’ve mistakenly run the following command by typing jg instead of jpg
md5sum *.jg | cut -c1-32 | sort | uniq -c | sort -nr
md5sum: '*.jg': No such file or directory


# METHOD 1
# To run the command properly, you could recall it from the command history, 
# cursor over to the mistake and fix it, but there’s a quicker way to accomplish your goal. 
# Just type the old (wrong) text, the new (corrected) text, and a pair of carets (^), like this
^jg^jpg
md5sum *.jpg | cut -c1-32 | sort | uniq -c | sort -nr
⋮

# METHOD 2
# similar to sed
# works with !! and !
!!:s/jg/jpg/
md5sum *.jpg | cut -c1-32 | sort | uniq -c | sort -nr
⋮
OR
!md5sum:s/jg/jpg/
md5sum *.jpg | cut -c1-32 | sort | uniq -c | sort -nr
⋮
```