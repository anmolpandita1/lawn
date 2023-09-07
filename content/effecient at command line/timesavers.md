---
tags:
  - bash
  - cli
---
```bash
# When you’re viewing a text file with less and want to edit the file, don’t exit less. 
# Just press v to launch your preferred text editor.
# Set the environment variable EDITOR and/or VISUAL to an editing command.

Learn rsync
To copy a full directory, including its subdirectories, from one disk location to another, many Linux users turn to the command cp -r or cp -a:

$ cp -a dir1 dir2
cp does the job fine the first time, but if you later modify a few files in directory dir1 and perform the copy again, cp is wasteful. It dutifully copies all files and directories from dir1 all over again, even if identical copies already exist in dir2.

The command rsync is a smarter copy program. It copies only the differences between the first and second directories.

$ rsync -a dir1/ dir2
NOTE
The forward slash in the preceding command means to copy the files inside dir1. Without the slash, rsync would copy dir1 itself, creating dir2/dir1.

If you later add a file to directory dir1, rsync copies just that one file. If you change one line inside a file in dir1, rsync copies that one line! It’s a huge time-saver when copying large directory trees multiple times. rsync can even copy to a remote server over an SSH connection.

rsync has dozens of options. These are some particularly useful ones:

-v (meaning “verbose”)
To print the names of files as they’re copied

-n
To pretend to copy; combine with -v to see which files would be copied

-x
To tell rsync not to cross filesystem boundaries

I highly recommend getting comfortable with rsync for more efficient copying. Read the manpage and view examples in the article “Rsync Examples in Linux” by Korbin Brown.

```