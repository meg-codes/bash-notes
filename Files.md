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

## Moving a file - `mv`

`mv` moves a file, which in UNIX-land is also how you rename a file.

The basic syntax is `mv <source> <destination>`, in any format, relative or absolute that is valid.

`mv` is incredibly powerful and if you're moving around a lot of files will let you pull out some
really annoying problems. Once you're used to it, it's also much quicker than lassoing files with a mouse.

It can also end up sending files willy-nilly. Most operating system files are protected and require superuser privileges to edit or move, so unless you use `sudo`, you're unlikely to bring down your system. You
just might move some files somewhere annoying, however, so be careful.

The wildcard selector `*` and braces `{}` are both supported, too, huzzah!

Suppose you had a tremendously messy directory and needed to get all the text files out and put them elsewhere.

```
~/junkdrawer $pwd
/Users/benjaminhicks/junkdrawer
~/junkdrawer $ls -al
total 0
drwxr-xr-x   19 benjaminhicks  staff   646 Nov 28 12:56 .
drwxr-xr-x+ 131 benjaminhicks  staff  4454 Nov 28 12:54 ..
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 1.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 1.useful.txt
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 10.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 11.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 12.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 2.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 2.useful.txt
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 3.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 3.useful.txt
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 4.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 4.useful.txt
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 5.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 5.useful.txt
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 6.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 7.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 8.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 9.spam
~/junkdrawer $mkdir useful_text
~/junkdrawer $mv *.txt useful_text/
~/junkdrawer $ls -al
total 0
drwxr-xr-x   15 benjaminhicks  staff   510 Nov 28 12:57 .
drwxr-xr-x+ 131 benjaminhicks  staff  4454 Nov 28 12:54 ..
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 1.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 10.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 11.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 12.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 2.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 3.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 4.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 5.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 6.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 7.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 8.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 9.spam
drwxr-xr-x    7 benjaminhicks  staff   238 Nov 28 12:57 useful_text
~/junkdrawer $ls -al useful_text/
total 0
drwxr-xr-x   7 benjaminhicks  staff  238 Nov 28 12:57 .
drwxr-xr-x  15 benjaminhicks  staff  510 Nov 28 12:57 ..
-rw-r--r--   1 benjaminhicks  staff    0 Nov 28 12:56 1.useful.txt
-rw-r--r--   1 benjaminhicks  staff    0 Nov 28 12:56 2.useful.txt
-rw-r--r--   1 benjaminhicks  staff    0 Nov 28 12:56 3.useful.txt
-rw-r--r--   1 benjaminhicks  staff    0 Nov 28 12:56 4.useful.txt
-rw-r--r--   1 benjaminhicks  staff    0 Nov 28 12:56 5.useful.txts
```

The wildcard selector grabbed all the files that ended in .txt and then `mv` shunted them to the directory we made called `useful_files`.

The same flags `-r` and `-rp` and `-a` all apply to `mv` just as they did to `cp`. This is also how you rename a directory.

In the example above, `mv -r useful_text/ new_text/` would rename the directory to `new_text`

## Deleting a file - `rm`

### Caution
The `rm` command does NOT come with an undo. If you delete and don't have a backup, it's gone short of using a hard disk recovery tool and hoping the deleted blocks don't get overwritten. Be careful. If you use `sudo` be very, very careful. If someone tells you to `sudo rm -rf /*`, they're playing an old prank
involving deleting the subdirectories of the system root. Many modern Linux distros will prevent this,
as will MacOS, but just don't.

`rm`, as the caution above indicates, deletes files. Without flags, it will only delete files not directories, but it does accept the standard `*` and `{}` operators.

The syntax is `rm <file or list of files>`

On some systems, the `rm` command is re-aliased to `rm -i`. This is a nicety because it forces you to say yes or no to file deletions. On many, it is not so aliased and it will delete files aggressively and silently. If you're not sure what your `rm` is going to do, `rm -i` is useful to keep you from nuking files youwould really rather have.

Continuing from the example above, if I wanted to get rid of all the .spam files:

```
~/junkdrawer $ls -al
total 0
drwxr-xr-x   15 benjaminhicks  staff   510 Nov 28 12:57 .
drwxr-xr-x+ 131 benjaminhicks  staff  4454 Nov 28 13:00 ..
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 1.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 10.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 11.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 12.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 2.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 3.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 4.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 5.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 6.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 7.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 8.spam
-rw-r--r--    1 benjaminhicks  staff     0 Nov 28 12:56 9.spam
drwxr-xr-x    7 benjaminhicks  staff   238 Nov 28 12:57 useful_text
~/junkdrawer $rm *.spam
~/junkdrawer $ls
useful_text
~/junkdrawer $
```

Now, let's say I wanted to get rid of the whole junkdrawer folder. Here you'll need to use the familiar `-r` flag.

```
~/junkdrawer $cd ..
~ $rm -r junkdrawer/
``` 

I moved up one directory using `cd ..` and then `rm -r junkdrawer/` removed the folder and all its subfolders.

Some useful flags:

`rm -f` (and combinable as `rm -rf`) - These delete a file (or files/directories with `-r`) and also override any prompts for confirmation, which will still be offered based on the files permissions. This is a bulldozer. Aim carefully.

`rm -P` - This flag, also combinable, does a triple-overwrite of a file after deleting it, which can render it unrecoverable more quickly as a matter of security. You're not going to need this often.

 
 
