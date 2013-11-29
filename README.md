## Command line one-liners

After my blog post about [command line one-liners],
many people want to contribute with their own commands.
This is the place to do it, pull request are welcome!


Run the last command

    $ !!

Run the last command as root

    $ sudo !!

Create a script of the last executed command

    $ echo "!!" > script.sh

Reuse all parameter of the previous command line

    $ echo cd .
    $ !*

Run the last command with some argument

    $ echo a b c d e
    $ echo !!:2
    $ echo !!:3-$

Insert the last argument of the previous command

    $ cp script.sh /usr/bin/
    $ cd <ESC> .

Runs previous command but replacing

    $ echo no typos
    $ ^typos^errors

Escape any command aliases

    $ alias ls="ls -a"
    $ \ls

Quickly rename a file

    $ mv filename.{old,new}
    $ mv filename.{png,jpg}

Create a quick back-up copy of a file

    $ cp file.txt{,.bak}

Run a command from the history

    $ history
     ...
     1225  ls -l
     1226  git status
     1227  history
    $ !-3
    $ !1225

Search the history for the most recent command beginning with 'text'

    $ !text

List of commands you use most often

    $ history | awk '{print $2}' | sort | uniq -c | sort -rn | head

Execute a command without saving it in the history

    $ <space>command

Make directory including intermediate directories

    $ mkdir -p a/long/directory/path

Create a directory and change into it

    $ mkdir dir && cd $_

Change to the previous working directory

    $ cd -

Jump to a directory. Execute a command. Jump back to current directory

    $ (cd /tmp && ls)

Create simple text file from command line

    $ cat > file.txt
    {your text here}
    {your text here}
    <ctrl-d>

Empty a file

    $ > file.txt

Show PATH in a human-readable way

    $ echo $PATH | tr ':' '\n'
    $ tr ':' '\n' <<< $PATH

Make 'less' behave like 'tail -f'

    $ less +F somelogfile

Redirect standard input to a file. Print it to standard output

    $ command | tee file.txt | less

    ┌─────────┐  ┌─────────┐  ┌─────────┐
    │ command │─▸│   tee   │─▸│ stdout  │
    └─────────┘  └────┬────┘  └─────────┘
                      │
                      ▾
                ┌───────────┐
                │   file    │
                └───────────┘

Search for a <pattern> string inside all files in the current directory

    $ grep -RnsI --color=auto <pattern> *

Beyond grep

    _   /|
    \'o.O'
    =(___)=
      U    ack!

    $ ack <pattern>

Recursively remove all empty directories

    $ find . -type d -empty -delete

Count your commits

    $ git shortlog -sn

Serve current directory tree at http://$HOSTNAME:8000/

    $ python -m SimpleHTTPServer

Share a file between two computers

    $ nc -l 5566 > data-dump.sql
    $ nc <his-ip-address> 5566 < data-dump.sql

Download an entire website

    $ wget -m http://website.com

Clear the terminal screen

    <ctrl-l>

Salvage a borked terminal

    $ reset

Close shell keeping all subprocess running

    $ disown -a && exit

Run a command immune to hangups

    $ nohup command &

Attach screen over ssh

    $ ssh user@host -t screen -r

Compare a remote file with a local file

    $ ssh user@host cat /path/to/remotefile | diff /path/to/localfile -

Get your public IP address

    $ curl ifconfig.me

Set audible alarm when an IP address comes online

    $ ping -a IP_address

List programs with open ports and connections

    $ lsof -i

Currently mounted filesystems in nice layout

    $ mount | column -t

Display free disk space

    $ df -h

Display disk usage statistics for the current directory

    $ du -sh *

Display 10 biggest files/folders for the current directory

    $ du -s * | sort -nr | head

Execute a command at a given time

    $ echo "ls -l" | at midnight

Simple stopwatch

    $ time read
    <ctrl-d>

Put a console clock in top right corner

    $ while sleep 1;do tput sc;tput cup 0 $(($(tput cols)-29));date;tput rc;done &

Display the top ten running processes. (Sorted by memory usage)

    $ ps aux | sort -nk +4 | tail

Kill all Ruby processes

    $ ps aux | grep ruby | awk '{ print $2 }' | xargs kill -9
    $ ps aux | awk '/ruby/ && ! /awk/ { system("kill -9 "$2) }'

32 bits or 64 bits?

    $ getconf LONG_BIT

Displays a calendar

    $ cal 12 1984

What day is today?

    $ cal | sed "s/.*/ & /;s/ $(date +%d) / [] /"
    $ cal | sed "s/.*/ & /;s/ $(date +%d) / $(printf '\e[0;31m[]\e[0m') /"

Show File System Hierarchy

    $ man hier

Quick access to the ascii table

    $ man ascii

Russian Roulette in Bash

    $ [ $[ $RANDOM % 6 ] == 0 ] && rm -rf / || echo "You live"

Watch Star Wars via telnet

    $ telnet towel.blinkenlights.nl


[command line one-liners]: http://arturoherrero.com/2013/11/29/command-line-one-liners/
