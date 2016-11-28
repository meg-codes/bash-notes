# Working with Files

## A Word about Files in Unix

In the world of UNIX systems (Linux, MacOS, FreeBSD, etc.), files are really onl of two types: 1) Binary and 2) Text.
This philosophy carries through to the commandline also. You can think of the BASH shell as a way of working with files that
are often nothing more than a stream of text.

## Copying a file - `cp`

`cp` is a command that lets you, well, copy a file. The syntax is relatively straightfoward but it does have a few 
useful flags to know.

`cp <file> <newfile>` is the basic syntax. The file can be given as a relative path or an absolute one (see [Directories](Directories.md) if this doesn't make sense).


`cp` also supports wildcard expansion, so the characters `*` and `{}` both have special meanings.

If you wanted to copy all the files in one directory, for example:

```
~/foo $pwd
/Users/benjaminhicks/foo
~/foo $ls -al

total 0
drwxr-xr-x    6 benjaminhicks  staff   204 Nov 28 12:37 .
drwxr-xr-x+ 130 benjaminhicks  staff  4420 Nov 28 12:37 ..
drwxr-xr-x    2 benjaminhicks  staff    68 Nov 28 12:40 bar
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:37 file1
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:37 file2
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:37 file3

~/foo $cp * bar/
cp: bar is a directory (not copied).
~/foo $ls -al bar/

total 0
drwxr-xr-x  5 benjaminhicks  staff  170 Nov 28 12:42 .
drwxr-xr-x  6 benjaminhicks  staff  204 Nov 28 12:37 ..
-rw-r--r--  1 benjaminhicks  staff    0 Nov 28 12:42 file1
-rw-r--r--  1 benjaminhicks  staff    0 Nov 28 12:42 file2
-rw-r--r--  1 benjaminhicks  staff    0 Nov 28 12:42 file3
```

Since we didn't use recursion, you'll note that the wildcard `*` also selected bar underneath. By default
it matches ANY character. To avoid this (and also some potentially hilarious recursion loops if you just 
say directories are OK using `-r`), you can be more targeted.

In this instance `cp file* bar/` would work very well. You could also use `cp {file1,file2,file3} bar/`
since `{}` with commas and no spaces as separators gets expanded into running `cp file1 bar/ cp file2 bar/`, etc.  


A few important flags:
* `cp -r` - This sets `cp` to copy recursively, i.e. it lets you copy an entire directory and all the subdirectories below it.
 - For example: `cp -r foo/ bar/` would copy the entire directory `foo/` and all its subdirectories and files to `bar/` relative to your working directory.
* `cp -rp` or `cp -a`:
 - Similar commands, these are recursive AND ensure that the files are copied with the same owner and permissions. `cp -a` combines all of these and preserves some Linux security features. 
