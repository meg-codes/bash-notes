# Command Line Cheat Sheet

## What this is document and isn't
This document is a basic guide to getting around the file system of a POSIX (Unix, Linux,
MacOS based system). It is not comprehensive.

It is also geared primarily to POSIX based systems (though Windows 10 users
should note that an Ubuntu command line now exists for it, too!).

## Getting to a terminal
Pulling up a command line terminal varies from operating system to operating system.
On MacOS, the Terminal app launches the command line, whereas various flavors of Linux
will hide it in various places if launched in workstation (graphical) mode.

When logging on to a server or computing cluster via an SSH client, you'll
simply land in a terminal.

Most likely the shell you'll encounter is the one whose commands are described herein,
the Bash shell (Bourne Against SHell), a revision of the older SH. There are
different flavors of Bash, and different Unix-based OSes all have their tics.

## What is a shell?
A shell is an operating utility that provides some basic facility for running other programs
and ultimately, moving text from one place to another. (One of the fundamental principles
of a POSIX environment is that most configuration files are, in some form or another, just
text.)

You will launch programs by invoking their name. A certain class of programs are kept in
directories that your operating system knows to look in, and they can be invoked by just their
bare name. It's the equivalent of clicking on shortcut to an application in your Applications folder in a
graphical interface. We can adjust that using a special setting (called a variable) in
our environment, called `$PATH`. You do not want to start editing that until you have a good
sense of what you're doing, as you can render it difficult to use any commands whatsoever.

(Not permanently, even if you do mess up. As with most things, it is fixable.)

Most commands will follow a pattern that looks something like this:

```
program_name -f --flag argument1 argument2
```

Where `-f` is what we call a short flag, i.e. a quick modification to how the program runs and
`--flag` is its spelled-out form. (They're functionally equivalent, but you can often stack
the shortened form together, i.e. `ls -al`).

Arguments are often files. For example to echo the contents of a file to the command line, I can type:

```
cat myfile.txt
```

`myfile.txt` is the first argument of the program `cat`, which conCATenates the contents of
of a list of files.

## Always use 'man'.
One of the most useful commands you should probably learn before even basic
file operations is the most straightfoward -- 'man'

Syntax:

```bash
man <command>
```
It will give a printout of a particular system command's usage
(or really any program that has manual documentation) to the terminal window

A shortened version of the output of `man ls` is here:
```
LS(1)                     BSD General Commands Manual                    LS(1)

NAME
     ls -- list directory contents

SYNOPSIS
     ls [-ABCFGHLOPRSTUW@abcdefghiklmnopqrstuwx1] [file ...]

DESCRIPTION
     For each operand that names a file of a type other than directory, ls dis-
     plays its name as well as any requested, associated information.  For each
     operand that names a file of type directory, ls displays the names of files
     contained within that directory, as well as any requested, associated infor-
     mation.

     If no operands are given, the contents of the current directory are dis-
     played.  If more than one operand is given, non-directory operands are dis-
     played first; directory and non-directory operands are sorted separately and
     in lexicographical order.
```

Most entries describe the command's basic function, give a listing of its operands
(usually prefixed by `--` or `-``) and then what it takes as an input.

So from that, we learn that `ls` lists the contents of a directory.

## Getting around the file system

When you first open a terminal, you will probably be dropped off in your home directoy,
often abbreviated by a `~`. POSIX systems all use forward slashes to mark directory
structure. (Directories are like the folders you see in a graphical interface.)

For example:
```
/ denotes the root directory (all directories stem from this)
/home/ marks a directory under the directory /
/home/user marks a directory under /home
```

The prompt for my home directory on a server called della is something like this:
```
[bhicks@della4 ~]$
```
The $ is just shell speak for 'Ready to start a new command' and 'you are not the root user'
(the root or a superuser can modify system or other restricted files)

Let's look around, shall we? If you see a command here, run its 'man' to get a
full listing. It's habit building. In a good way.

### Looking around - `ls` and `pwd`
`ls` gives you the structure of a directory and its files.

Without any arguments, it will return any non-hidden files in your current directory.

```
[bhicks@della4 ~]$ ls
output.out  R  R-benchmark-25.R  R-benchmark-parallel.R  Rmpi_0.6-6.tar.gz  submit.cmd
```

This shows me a list of files in the current directory, but not much else.

A useful common set of operands are `ls -al`:
```
[bhicks@della4 ~]$ ls -al
total 248
drwxr-xr-x  12 bhicks cses   4096 Nov  7 14:59 .
drwxr-xr-x 758 root   root  20480 Nov  7 14:24 ..
-rw-------   1 bhicks cses  11732 Nov  7 15:16 .bash_history
-rw-r--r--   1 bhicks cses     18 Jul 20 11:16 .bash_logout
-rw-r--r--   1 bhicks cses    192 Nov  7 13:07 .bash_profile
-rw-r--r--   1 bhicks cses    231 Jul 20 11:16 .bashrc
-rw-r--r--   1 bhicks cses   1448 Oct 27 13:12 .c
drwx------   6 bhicks cses     84 Sep  6 08:58 .cache
drwxr-xr-x   3 bhicks cses     40 Aug  2 11:57 .conda
drwxr-xr-x   3 bhicks cses     44 Sep  6 09:07 .config
-rw-r--r--   1 bhicks cses     37 Oct 27 12:13 .gitconfig
-rw-r--r--   1 bhicks cses    172 Jul 20 11:16 .kshrc
drwx------   5 bhicks cses     51 Aug  2 08:59 .local
drwxr-xr-x   3 bhicks cses     55 Sep  6 09:06 .matplotlib
-rw-r--r--   1 bhicks cses  10432 Oct 27 13:12 .o
-rw-r--r--   1 bhicks cses    422 Nov  7 14:58 output.out
drwxr-xr-x   2 bhicks cses     28 Aug  2 12:29 .pip
drwxr-----   3 bhicks cses     26 Sep  6 08:56 .pki
drwxr-xr-x   3 bhicks cses     44 Nov  4 12:27 R
-rw-r--r--   1 bhicks cses  13666 Dec  2  2012 R-benchmark-25.R
-rwxr-xr-x   1 bhicks cses   3052 Nov  7 14:21 R-benchmark-parallel.R
-rw-r--r--   1 bhicks cses 105181 Jun  2 09:11 Rmpi_0.6-6.tar.gz
-rw-r--r--   1 bhicks cses     48 Nov  4 12:26 .R.Rout
-rwxr-xr-x   1 bhicks cses  11429 Oct 27 13:12 .so
drwx------   2 bhicks cses     24 Sep 27 14:40 .ssh
-rw-r--r--   1 bhicks cses    378 Nov  7 14:58 submit.cmd
drwxr-xr-x   2 bhicks cses     31 Oct 27 11:17 .vim
-rw-------   1 bhicks cses   5282 Nov  7 14:59 .viminfo
-rw-------   1 bhicks cses     50 Sep  6 09:02 .Xauthority
```

This looks like a lot of obtuse information, but it tells me 1) all the files, including
'hidden' dotted files like my .bashrc that helps set initial variables for a Bash session 2) shows size in B (add -alh to get a more useful set of values there) and 3) the
permissions of each file, but that's a topic for later. You'll also note that `-a` is the
flag for 'alphabetical'.

I still don't know what the absolute file path for the directory is. In this case,
`pwd` is the ticket. It prints the working directory to the console.

```
[bhicks@della4 ~]$ pwd
/home/bhicks
```

Now I know that ~ is a shorthand way of writing /home/bhicks.

## You are now free to move about the file system - `cd`

I know where I am. Now how do I get where I'm going? `cd` is the command to change the working directory in a POSIX environment.

The basic syntax is `cd <new directory>`. But here we can get into what those `.` and `..` at the top of a directory listing mean.

`.` marks the current directory and its permissions.
`..` marks the directory above.

You can use these as a quick shorthand in many cases.

If I were in `/home/bhicks` then `cd ..` would move me to `/home`. You can keep doing this, or even chain them. From `/home/bhicks` `cd ../..` would move me to ``/``.

You can also use `cd` to move to an absolute or relative path. An absolute path is a path written from root down (`/var/www/public_html/images/cat_gifs`). A relative path is written from the current directory (if your working dir was `/var/www`, then `cd public_html/images/cat_gifs` would get you to the same directory as the absolute path above).

It's worth noting that this distinction applies to any command where you supply a file name for execution. `cp /home/bhicks/interlac_dict.txt /home/fnord/` and `cp interlac_dict.txt /home/fnord` would work equally well--if my working directory were `/home/bhicks`.

## Making a new folder - `mkdir`

The aptly named `mkdir` will make a directory. The syntax is `mkdir <directory name>`. It has a few quirks.

Let's say I'm in my home directory and want to make a folder and a folder beneath it.

```
~ $mkdir work
~ $mkdir work/Mon
```

Great! The folders `~/work` and `~/work/Mon` now both exist.

So, you might think, 'I bet I can just do `mkdir work/Mon`!` to save a step. But you'll get this if you're starting from scratch.

```
~ $mkdir work/Mon
mkdir: work: No such file or directory
```

Sounds like a Monday. In any case, `mkdir` can't make the subdirectory because the directory doesn't exist.  However: `mkdir -p work/Mon` works like a charm. The `-p` flag creates subdirectories recursively.

You can combine this with the `{}` braces selector to do some neat tricks. `mkdir -p work/{Mon,Tues,Wed,Thurs,Fri}` will create `work/` and then the named subdirectories below, all in one shot.
