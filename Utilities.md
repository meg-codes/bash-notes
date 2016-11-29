# Utiliites for working with files

Listed below are an entirely non-comprehensive list of utilities you can use to do useful things with files. Many rely on a concept discussed below called a 'regular expression'. If you aren't familiar with these, I have linked some explanations of different regex flavors and implementations.

Others are just useful for watching processes and files.

## Regexes

Regular expressions are a shorthand way of telling a scripting language (or really any language) or utility 'look for this match'.

This can be very useful for finding a line that matches and deleting it, finding and replacing text (your word processor's find and rreplace is a much more use friendly but often less powerful version of this), etc.

Many programming languages have their versions of the regex, all of which tend to look similar but have different features. If you need highly complex regex, you're probably better moving to a scripting language like Python, PHP, or Javascript--or even a data science tool like R. 

The two BASH tools I'll discuss that use regexes to great benefit are `grep` and `sed`.

The less than newbie friendly guide to regexes for the two programs are linked here:
[`sed` regexes](https://www.gnu.org/software/sed/manual/html_node/Regular-Expressions.html)
[`grep` regexes](https://www.cyberciti.biz/faq/grep-regular-expressions/) 
	Note: This site also explain the difference in `grep -E` and `grep -F`, which are on old systems sometimes different commands.

[`grep` regex checker](https://www.online-utility.org/text/grep.jsp)

## Checking what you did - `history`

`history` is a highly, highly useful command. It prints the contents of the hidden file `.bash__history` (usually in `~`) to the console along with a list of numbers.

You can shortcut this for the previous command without typing anything by just pressing the up arrow. Rinse and repeat the command.

But say you wanted to do this for something 50 back? You could hit up 50 times, or you cann call `history` and note the number. Then at a new terminal just type `!number` where number is the number of the command. It will be printed to the command line to be used again!

You can also pipe history output to `grep`, which I go into more detail later, but this is an easy usage:

Say I wanted to know 'When was the last time I ran a script named "manage.py"?'

`history | grep manage.py` would search my user history and return any lines that had
"manage.py" in them, matched strictly.


## Looking at text - `less`, `tail`, and `head`

You might find yourself wanting a look at a file, but not wanting to fire up a text editor like `vim` (often aliased to `vi`)  or `nano`. You could `echo` or `cat` the file to the terminal, but you can't scroll or search that, which makes it somewhat worthless.

Here are some options:

### `less` isn't `more`
 
The history of this commandline utility is somewhre beyond confusing. It postdates `more`, which was a less flexible version of the pgining utility (i.e. utilities that take text and paginate it for display), but it predates the less common utility `most`. To quote the [Slackware Linux Essentials Guide](http://www.slackbook.org/html/file-commands-pagers.html): 'If `less` is more than `more`, `most` is more than `less`.

If your platform has `most` installed, it's worth looking through the `man` page and learning about it. It lets you open multiple file buffers at once, among other niceties.

`less` is the goto butter-knife here.

The syntax is simply `less <filename>`, i.e. `less myfile.html`

This will open any file, but of course a binary file (vs. HTML, XML, text documents, etc.) will just be gibberish.

`less` will take over your terminal and let you scroll up and down in the buffer. You can use `q` to quit and `:` to start command sequences. `:/regex` will let you search for a word in the file you've opened.

The `man` page goes into much greater detail as to manuevering `less`. It is very handy.

### `grep`

Don't worry about the name. `grep` is amazing and it will revolutionize how you look at files. Its usage is really beyond this basic overview, so I've included some links below. 
