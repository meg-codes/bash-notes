# Working with files, piping input, etc.

## The wonderful world of the tty
The terminal window, running BASH or another shell, is essentially a stream of text. It sends input and output to two basic 'pipes', `stdin` and `stdout`. `stdout` is what you see when you run a command.

`stderr` is often where messages are passed for errors. It too will put in an appearance on the commandline.

`stdin` is data that's piped to a program. More on this later.

On the terminal, you have control over where these outputs go--be that another program, a file, or nowhere at all.

This is where the magic happens. But first...

## Making a dummy file - `touch`
If you've wondered why many of my examples have empty files, that's because I created them using the `touch` command. It well, touches a file. Like the scene from E.T. but much less moving. This create an entry
in the file system and a blank (text) file.

`touch <filename and path>` is pretty straightforward. You can also use Bash scripting tricks to do more
complicated things, but this program is just worth a mention.

## Redirecting and piping - `>`, `<`, `|`
These characters let you tell the shell what to send where.

### `OUTPUT > file`

The `>` character lets you redirect `stdout` to any file. If you type `ls -alh > dir_listing.txt`, for eample, you'll make a file named dir_listing.txt in your working directory that has the output of the `ls`.

This lets you pull off really interesting short hand ways of doing things. Say, for example, you have a
pile of text documents that you need to combine into one. You can use the `cat` command, which conCATenates files, to combine them into one using `>`.

If the files all happened to end in .txt, you could do `cat *.txt > combined.txt`. The new file would have the contents of all files whose names end in .txt in your current working directory.

This creates the file or overwrites it if it does exist.

`>>` changes the mode to make it append to the file if it does exist.

### `COMMAND  < file `

This takes a file and pushes it to a command. Many commands take file arguments and shorthand this, but yo can always do it expressly.


### Complex redirects
You can also use these commands to redirect the terminal output too. This can be useful for keeping logs
or silencing a command you'd just as soon not see the output of.

`1` is the number for `stdout` and `2` is the one for `stderr`. 

`1>filename` redirects `stdout` to `filename`
`2>filename` does the same thing for `stderr`

`2>&1` redirects `stderr` to `stdout` and you can then dump the whole shebang. You'll usually append this modifier after the command.

`blah > output_log 2>&1` will produce a file named `output_log` that will gripe about there not being a blah command.

If you want to silence output entirely, ` blah > /dev/null 2>&1 ` will send the output to the null device,
a round-about way of saying 'toss the whole thing, I don't care'.


### Down the pipe - `|`

The most useful tool you'll encounter is the `|`. This pipes the standard output of one program to another (`2>&1` at the end of your command will redirect `stderr` too).

Why would I want to do this? An excellent example is the `find` command. Without going into its complex
(and implementation specific) syntax, `find .` would start in your current directory and recursively list every single file (throwing errors for files you don't have permission to read).

Not hugely useful as a search, but you can then pull out the handy-dandy tool of the Unix world: `grep`.

The name is somewhat useless, but its basic purpose is this: to search for a pattern in a file OR stream
you specify.

I do a lot of work on a Roman author named Pliny. Let's say I totally forgot this fact and wanted to find every file, folder, and subfolder in my home dir that used his name .

I'd `cd ~`, then run `find . | grep pliny`. By default, grep returns any line where it finds a match for the regular expression (long story, to be explained later) I feed it.

Now, if I wanted to keep this list: `find . | grep pliny > search.txt`.


 



