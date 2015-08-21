---
layout: post
date:   2015-08-09 13:00:00
categories: linux
---
* will be replace by toc
{:toc}

# Getting started
===================

##1.2 Connect to server
-l = user name
-X = tunnel X over ssh

~~~ bash
ssh -l oracle -X -p 22 server1
~~~

##1.3 Logout

~~~ bash
ctrl-D
logout
exit
~~~~

##1.4 Check disk space
-h = human readable

~~~ bash
df -h /dev/sda1
~~~

##1.5 Getting help

~~~ bash
man -f cd
man 1p cd
man find | col -b >find.txt
ls /bin | xargs whatis | less
whereis echo
~~~

##1.6 Correcting command line mistakes

~~~ bash
ctrl+_ # undo
ctrl+u  # clear left
ctrl+t # transpose
alt+t
~~~~

##1.7 Reset screen

~~~ bash
reset
stty sane
~~~

#2. Shell

##2.1 Command history

~~~ bash
ctrl-n/p
ctrl-r
set -o vi
~~~

##2.3 View current env variables

~~~ bash
printenv,env,set,export,echo
PATH, USER, HOME, PWD, SHELL, EDITOR, PS1, SHLVL, DISPLAY
echo $SHELL = echo $0 = ps
~~~~

##2.5 bash configuration

. = source

~~~ bash 
#in ~/.bash_profile
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi
# typical entries
# No core files by default
ulimit -S -c 0 > /dev/null 2>&1
# Set OS variables
USER="`id -un`"
LOGNAME=$USER
MAIL="/var/spool/mail/$USER"
HOSTNAME=`/bin/hostname`
~~~

