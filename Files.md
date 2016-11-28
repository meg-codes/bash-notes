# Working with Files

## A Word about Files in Unix

In the world of UNIX systems (Linux, MacOS, FreeBSD, etc.), files are really onl of two types: 1) Binary and 2) Text.
This philosophy carries through to the commandline also. You can think of the BASH shell as a way of working with files that
are often nothing more than a stream of text.

## Copying a file - `cp`

`cp` is a command that lets you, well, copy a file. The syntax is relatively straightfoward but it does have a few 
useful flags to know.

`cp <file> <newfile>` is the basic syntax. The file can be given as a relative path or an absolute one (see [Directories](Directories.md)) if this 
doesn't make sense.

A few important flags:
* `cp -r` - This sets `cp` to copy recursively, i.e. it lets you copy an entire directory and all the subdirectories below it.
 - For example: `cp -r foo/ bar/` would copy the entire directory `foo/` and all its subdirectories and files to `bar/` relative to your working directory.
* `cp -rp` or `cp -a`:
 - Similar commands, these are recursive AND ensure that the files are copied with the same owner and permissions. `cp -a` combines all of these and preserves some Linux security features. 
