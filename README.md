# Command line one-liners

After my article about [command line one-liners][1], many people want to
contribute with their own commands. This is the place to do it, pull requests
are welcome!

## Table of Contents

- [History](#history)
- [Directories](#directories)
- [Files](#files)
- [Searching](#searching)
- [Networking](#networking)
- [User environment](#user-environment)
- [File system](#file-system)
- [Date & Time](#date--time)
- [Processes](#processes)
- [Miscellaneous](#miscellaneous)

- - -

### History

- Run the last command

  ```
  $ !!
  ```

- Run the last command as root

  ```
  $ sudo !!
  ```

- Create a script of the last executed command

  ```
  $ echo "!!" > script.sh
  ```

- Reuse all parameter of the previous command line

  ```
  $ echo cd .
  $ !*
  ```

- Run the last command with some argument

  ```
  $ echo a b c d e
  $ echo !!:2
  $ echo !!:3-$
  ```

- Insert the last argument of the previous command

  ```
  $ cp script.sh /usr/bin/
  $ cd !$
  $ cd <ESC> .
  $ cd <ALT> .
  ```

- Runs previous command but replacing

  ```
  $ echo no typos
  $ ^typos^errors
  ```

- Escape any command aliases

  ```
  $ alias ls="ls -a"
  $ \ls
  ```

- Run a command from the history

  ```
  $ history
     ...
     1225  ls -l
     1226  git status
     1227  history
  $ !-3
  $ !1225
  ```

- Search the history for the most recent command beginning with `text`

  ```
  $ !text
  ```

- Search the history for the most recent command containing `text`

  ```
  $ <ctrl-r>text
  ```

- List of commands you use most often

  ```
  $ history | awk '{print $2}' | sort | uniq -c | sort -rn | head
  ```

- Execute a command without saving it in the history

  ```
  $ <space>command
  ```


### Directories

- Make a directory creating intermediate directories

  ```
  $ mkdir -p a/long/directory/path
  ```

- Create a directory and change into it

  ```
  $ mkdir dir && cd $_
  ```

- Change to the previous working directory

  ```
  $ cd -
  ```

- Jump to a directory. Execute a command in a subshell. Jump back to current directory

  ```
  $ (cd /tmp && ls)
  ```


### Files

- Quickly rename a file

  ```
  $ mv filename.{old,new}
  $ mv filename.{png,jpg}
  ```

- Create a quick back-up copy of a file

  ```
  $ cp file.txt{,.bak}
  ```

- Create a simple text file from command line

  ```
  $ cat > file.txt
  {your text here}
  {your text here}
  <ctrl-d>
  ```

- Create a simple text file from command line or script (`EOF` is just a token, can be any word)

  ```
  $ cat > file.txt << EOF
  {your text here}
  {your text here}
  EOF
  ```

- Empty a file from command line (usefull to truncate log file from running processes)

  ```
  $ > file.txt
  ```

- Empty a file from command line or script

  ```
  $ cat /dev/null > file.txt
  ```

- Make `less` behave like `tail -f`

  ```
  $ less +F somelogfile
  ```

- Display line numbers in a file

  ```
  $ cat -n file
  $ less -N file
  ```

- Redirect standard input to a file. Print it to standard output

  ```
  $ command | tee file.txt | less

    ┌─────────┐  ┌─────────┐  ┌─────────┐
    │ command │─▸│   tee   │─▸│ stdout  │
    └─────────┘  └────┬────┘  └─────────┘
                      │
                      ▾
                ┌───────────┐
                │   file    │
                └───────────┘
  ```


### Searching

- Search for a <pattern> string inside all files in the current directory

  ```
  $ grep -RnsI --color=auto <pattern> *
  ```

- Beyond grep

  ```
    _   /|
    \'o.O'
    =(___)=
      U    ack!

  $ ack <pattern>
  ```

- Recursively remove all empty directories

  ```
  $ find . -type d -empty -delete
  ```


### Networking

- Serve current directory tree at `http://$HOSTNAME:8000/`

  ```
  $ python -m SimpleHTTPServer
  $ ruby -run -e httpd . -p 8000
  ```

- Share a file between two computers

  ```
  receiver $ nc -l 5566 > data-dump.sql
  sender   $ nc <receiver-ip-address> 5566 < data-dump.sql
  ```

- Share a BIG file between two computers and show progress bar

  ```
  receiver $ nc -l 5566 > big-file.iso
  sender   $ pv big-file.iso | nc <receiver-ip-address> 5566
  ```

- Transfer a folder between two computers

  ```
  receiver $ nc -l 5566 | tar -zxv
  sender   $ tar -zcv <folder> | nc -w1 <receiver-ip-address> 5566
  ```

- Download an entire website

  ```
  $ wget -m -k http://website.com
  ```

### User environment

- Show `PATH` in a human-readable way

  ```
  $ echo $PATH | tr ':' '\n'
  $ tr ':' '\n' <<< $PATH
  ```

- Clear the terminal screen

  ```
  $ <ctrl-l>
  $ clear
  ```

- Salvage a borked terminal

  ```
  $ reset
  ```

- Close shell keeping all subprocess running

  ```
  $ disown -a && exit
  ```

- Run a command immune to hangups

  ```
  $ nohup command &
  ```


### Networking

- Attach screen over ssh

  ```
  $ ssh user@host -t screen -r
  ```

- Compare a remote file with a local file

  ```
  $ ssh user@host cat /path/to/remotefile | diff /path/to/localfile -
  ```

- Get your public IP address

  ```
  $ curl ifconfig.me
  ```

- Set audible alarm when an IP address comes online

  ```
  $ ping -a IP_address
  ```

- List programs with open ports and connections

  ```
  $ lsof -i
  ```

- Check which process is listening on a specific port

  ```
  $ netstat -nlp | grep 8080
  $ netstat -nlp tcp | grep 8080 (BSD)
  ```


### File system

- Currently mounted filesystems in nice layout

  ```
  $ mount | column -t
  ```

- Display free disk space

  ```
  $ df -h
  ```

- Display disk usage statistics for the current directory

  ```
  $ du -sh *
  ```

- Display 10 biggest files/folders for the current directory

  ```
  $ du -s * | sort -nr | head
  ```

- Create a zip archive of a directory

  ```
  $ zip -r archive.zip directory
  ```

- Extract compressed archive

  ```
  $ unzip archive.zip
  ```

- Show File System Hierarchy

  ```
  $ man hier
  ```


### Date & Time

- Shutdown the system at a given time

  ```
  $ shutdown -h now
  $ shutdown -h 22:49
  ```

- Execute a command at a given time

  ```
  $ echo "ls -l" | at midnight
  ```

- Simple stopwatch

  ```
  $ time read
  <ctrl-d>
  ```

- Put a console clock in top right corner

  ```
  $ while sleep 1;do tput sc;tput cup 0 $(($(tput cols)-29));date;tput rc;done &
  ```

- Displays a calendar

  ```
  $ cal 12 1984
  ```

- What day was yesterday or will it be tomorrow, etc...

  ```
  $ date -d yesterday
  $ date -d tomorrow +%Y-%m-%d
  $ date -d "7 days ago" +%Y-%m-%d
  $ date -j -v-1d (BSD)
  ```


### Processes

- Display the top ten running processes. (Sorted by memory usage)

  ```
  $ ps aux | sort -nk +4 | tail
  ```

- Kill all Ruby processes

  ```
  $ ps aux | grep ruby | awk '{ print $2 }' | xargs kill -9
  $ ps aux | awk '/ruby/ && ! /awk/ { system("kill -9 "$2) }'
  $ pkill -f ruby
  $ killall -9 ruby
  ```

- Check which process is modifying a certain directory or file

  ```
  $ auditctl -w /path/to/directory -p war
  ```

  See results

  ```
  $ ausearch -f /path/to/directory
  ```


### Miscellaneous

- 32 bits or 64 bits?

  ```
  $ getconf LONG_BIT
  ```

- Quick access to the ascii table

  ```
  $ man ascii
  ```

- Count your commits

  ```
  $ git shortlog -sn
  ```

- Russian Roulette in Bash (remember kids don't try this at home)

  ```
  $ [ $[ $RANDOM % 6 ] == 0 ] && rm -rf / || echo "You live"
  ```

- Watch Star Wars via telnet

  ```
  $ telnet towel.blinkenlights.nl
  ```


## Who made this?

This was made by Arturo Herrero under the MIT License. Find me on Twitter
[@ArturoHerrero][2].


[1]: http://arturoherrero.com/command-line-one-liners/
[2]: https://twitter.com/ArturoHerrero
