# Bash and Shell Related Materials

This site contains a collection of notes relating to Bash for beginners that I've written.
Hopefully it can be a helpful resource, though at the moment it is primarily incomplete.

## Guides
[Basic file system directory commands - ls, pwd, cd, mkdir](Directories.md)

[Copying and (Re)Moving files - cp, mv, rm](Files.md)

[Input, Output, and Piping](Input.md)

[Utilities - less/head/tail, grep, sed](Utilities.md)

## Outside links and practice
[Codeacademy - Learn the command line](https://www.codecademy.com/learn/learn-the-command-line)

[command-line-bootcamp](http://rik.smith-unna.com/command_line_bootcamp/?id=nhgk0wnewbk)

Both of the above let you learn and test your commandline skills.

[Advanced Bash-Scripting Guide](http://www.tldp.org/LDP/abs/html/)

Despite the title, this assumes you have no programming knowledge. Bash scripting will let you automate and make remarkably complex programs using command line tools.

[Bash Cookbook](https://catalog.princeton.edu/catalog/10575576)

O'Reilly's excellent reference with examples of using Bash to carry out day to day tasks with
sample code. Good for when you ask yourself "How would I...?"

## Virtual Machine Resources
If you want to run Linux on a Windows platform that doesn't support WSL (anything pre-Win10), one option is to create a virtual machine with its own filesystem, etc. that runs on your physical machine as its host.

One of the easier, lightweight alternatives is [Vagrant](https://www.vagrantup.com/docs/installation/). Their documentation is reasonably good, and vagrant instances can be launched from the Windows Command Prompt.

Note: You will need Oracle's free [VirtualBox](https://www.virtualbox.org/wiki/Downloads) to facilitate the creation of the VMs for Vagrant.

This method can also be used on MacOS or Linux if you want to play with different distributions.
