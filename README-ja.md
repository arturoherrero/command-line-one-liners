<!--
## Command line one-liners
-->
##コマンドライン ワンライナー

<!--
After my blog post about [command line one-liners],
many people want to contribute with their own commands.
This is the place to do it, pull requests are welcome!
-->
[command line one-liners] についてのブログの投稿後、たくさんの方からコマンドの提供がありました。
そこで、こちらで受け付けることにしました。Pull Request 大歓迎です!


<!--
Run the last command
-->
直前のコマンドを実行する

    $ !!

<!--
Run the last command as root
-->
直前のコマンドを root 権限で実行する

    $ sudo !!

<!--
Create a script of the last executed command
-->
直前に実行したコマンドのスクリプトを作る

    $ echo "!!" > script.sh

<!--
Reuse all parameter of the previous command line
-->
直前のコマンドラインの全ての引数を再利用する

    $ echo cd .
    $ !*

<!--
Run the last command with some argument
-->
直前のコマンドに引数を与えて実行する

    $ echo a b c d e
    $ echo !!:2
    $ echo !!:3-$

<!--
Insert the last argument of the previous command
-->
直前のコマンドの最後の引数を挿入する

    $ cp script.sh /usr/bin/
    $ cd <ESC> .
    $ cd <ALT> .

<!--
Runs previous command but replacing
-->
直前のコマンドを置換して実行する

    $ echo no typos
    $ ^typos^errors

<!--
Escape any command aliases
-->
コマンドの別名 (エイリアス) をエスケープする

    $ alias ls="ls -a"
    $ \ls

<!--
Quickly rename a file
-->
手早くファイル名を変更する

    $ mv filename.{old,new}
    $ mv filename.{png,jpg}

<!--
Create a quick back-up copy of a file
-->
手早くファイルのバックアップコピーを作る

    $ cp file.txt{,.bak}

<!--
Run a command from the history
-->
履歴からコマンドを実行する

    $ history
     ...
     1225  ls -l
     1226  git status
     1227  history
    $ !-3
    $ !1225

<!--
Search the history for the most recent command beginning with 'text'
-->
履歴から 'text' で始まる直近のコマンドを検索する

    $ !text

<!--
Search the history for the most recent command containing 'text'
-->
履歴から 'text' を含む直近のコマンドを検索する

    $ <ctrl-r>text

<!--
List of commands you use most often
-->
利用頻度の高いコマンド一覧を表示する

    $ history | awk '{print $2}' | sort | uniq -c | sort -rn | head

<!--
Execute a command without saving it in the history
-->
履歴に記録せずにコマンドを実行する

    $ <space>command

<!--
Make directory including intermediate directories
-->
中間のディレクトリも含めてディレクトリを作成する

    $ mkdir -p a/long/directory/path

<!--
Create a directory and change into it
-->
ディレクトリを作成してそのディレクトリに移動する

    $ mkdir dir && cd $_

<!--
Change to the previous working directory
-->
直前の作業ディレクトリに移動する

    $ cd -

<!--
Jump to a directory. Execute a command in a subshell. Jump back to current directory
-->
ディレクトリを移動してサブシェル内でコマンドを実行し、元のディレクトリに戻る

    $ (cd /tmp && ls)

<!--
Create simple text file from command line
-->
コマンドラインから簡単なテキストファイルを作る

    $ cat > file.txt
    {your text here}
    {your text here}
    <ctrl-d>

<!--
Create simple text file from command line or script (EOF is just a token, can be any word)
-->
コマンドラインまたはスクリプトから簡単なテキストファイルを作る (EOF は単なるトークンです。任意の文字列が使えます)

    $ cat > file.txt << EOF
    {your text here}
    {your text here}
    EOF

<!--
Empty a file from command line (usefull to truncate log file from running processes)
-->
コマンドラインでファイルを空にする (実行中のプロセスからログファイルを切り詰めるのに便利です)

    $ > file.txt

<!--
Empty a file from command line or script
-->
コマンドラインやスクリプトからファイルを空にする

    $ cat /dev/null > file.txt

<!--
Show PATH in a human-readable way
-->
人が読みやすい形式で PATH を表示する

    $ echo $PATH | tr ':' '\n'
    $ tr ':' '\n' <<< $PATH

<!--
Make 'less' behave like 'tail -f'
-->
'tail -f' のように 'less' を動作させる

    $ less +F somelogfile

<!--
Redirect standard input to a file. Print it to standard output
-->
標準入力をファイルにリダイレクトし、標準出力に出力する

    $ command | tee file.txt | less

    ┌─────────┐  ┌─────────┐  ┌─────────┐
    │ command │─▸│   tee   │─▸│ stdout  │
    └─────────┘  └────┬────┘  └─────────┘
                      │
                      ▾
                ┌───────────┐
                │   file    │
                └───────────┘

<!--
Search for a <pattern> string inside all files in the current directory
-->
文字列 <pattern> をカレントディレクトリ内のすべてのファイルの中から検索する

    $ grep -RnsI --color=auto <pattern> *

<!--
Beyond grep
-->
grep を超えて

    _   /|
    \'o.O'
    =(___)=
      U    ack!

    $ ack <pattern>

<!--
Recursively remove all empty directories
-->
再帰的に空のディレクトリを全て削除する

    $ find . -type d -empty -delete

<!--
Count your commits
-->
自分のコミットを数える

    $ git shortlog -sn

<!--
Serve current directory tree at http://$HOSTNAME:8000/
-->
現在のディレクトリーツリーを http://$HOSTNAME:8000/ から公開する

    $ python -m SimpleHTTPServer

<!--
Share a file between two computers
-->
2 つのコンピュータ間でファイルを共有する

    receiver $ nc -l 5566 > data-dump.sql
    sender   $ nc <receiver-ip-address> 5566 < data-dump.sql

<!--
Share a BIG file between two computers and show progress bar
-->
2 つのコンピュータ間で巨大なファイルを共有し、プログレスバーを表示する

    receiver $ nc -l 5566 > big-file.iso
    sender   $ pv big-file.iso | nc <receiver-ip-address> 5566

<!--
Transfer a folder between two computers
-->
2 つのコンピュータ間でフォルダーを転送する

    receiver $ nc -l 5566 | tar -zxv
    sender   $ tar -zcv <folder> | nc -w1 <receiver-ip-address> 5566

<!--
Create an ISO image from a directory
-->
ディレクトリから ISO イメージを作る

    $ mkisofs -o my-backup.iso /a/directory/

<!--
Download an entire website
-->
あるウェブサイト全体をダウンロードする

    $ wget -m http://website.com

<!--
Clear the terminal screen
-->
ターミナル画面をクリアする

    <ctrl-l>

<!--
Salvage a borked terminal
-->
乱れたターミナル画面を復旧する

    $ reset

<!--
Close shell keeping all subprocess running
-->
全てのサブプロセスを実行したままシェルを閉じる

    $ disown -a && exit

<!--
Run a command immune to hangups
-->
ハングアップに反応しないようにしてコマンドを実行する

    $ nohup command &

<!--
Attach screen over ssh
-->
SSH 経由でスクリーンをアタッチする

    $ ssh user@host -t screen -r

<!--
Compare a remote file with a local file
-->
リモートのファイルとローカルのファイルを比較する

    $ ssh user@host cat /path/to/remotefile | diff /path/to/localfile -

<!--
Get your public IP address
-->
自分の公開 IP アドレスを表示する

    $ curl ifconfig.me

<!--
Set audible alarm when an IP address comes online
-->
指定した IP アドレスがオンライン上に存在する時にオーディオアラームを鳴らす

    $ ping -a IP_address

<!--
List programs with open ports and connections
-->
ポートを開放したり接続したりしているプログラムの一覧を表示する

    $ lsof -i

<!--
Check which process is listening on a specific port
-->
指定したポートを受け待ち (リッスン) しているプロセスを調べる

    $ netstat -nlp | grep 8080
    $ netstat -nlp tcp | grep 8080 (BSD)

<!--
Check which process is modifying a certain directory or file
-->
指定したディレクトリ、ファイルを修正しているプロセスを調べる

    $ auditctl -w /path/to/directory -p war
    # see results with:
    $ ausearch -f /path/to/directory

<!--
Currently mounted filesystems in nice layout
-->
マウント中のファイルシステムを整形して表示する

    $ mount | column -t

<!--
Hierarchy of available block devices
-->
利用可能なブロックデバイスの階層を表示する

    $ lsblk

<!--
Display free disk space
-->
ディスクの空き容量を表示する

    $ df -h

<!--
Display disk usage statistics for the current directory
-->
カレントディレクトリのディスク使用状況を表示する

    $ du -sh *

<!--
Display 10 biggest files/folders for the current directory
-->
カレントディレクトリのファイル/フォルダーを容量順に上位 10 件を表示する

    $ du -s * | sort -nr | head

<!--
Create a zip archive of a directory
-->
ディレクトリの zip アーカイブを作成する

    $ zip -r archive.zip directory

<!--
Extract compressed archive
-->
圧縮アーカイブを展開する

    $ unzip archive.zip

<!--
Execute a command at a given time
-->
指定した時間にコマンドを実行する

    $ echo "ls -l" | at midnight

<!--
Simple stopwatch
-->
簡単なストップウォッチ

    $ time read
    <ctrl-d>

<!--
Put a console clock in top right corner
-->
画面右上隅に時計を表示する

    $ while sleep 1;do tput sc;tput cup 0 $(($(tput cols)-29));date;tput rc;done &

<!--
Display the top ten running processes. (Sorted by memory usage)
-->
実行中のプロセスの上位 10 件を表示する (メモリー使用順)

    $ ps aux | sort -nk +4 | tail

<!--
Kill all Ruby processes
-->
全ての Ruby のプロセスを強制終了する

    $ ps aux | grep ruby | awk '{ print $2 }' | xargs kill -9
    $ ps aux | awk '/ruby/ && ! /awk/ { system("kill -9 "$2) }'
    $ pkill -f ruby
    $ killall -9 ruby

<!--
32 bits or 64 bits?
-->
32 bits か 64 bits か

    $ getconf LONG_BIT

<!--
Displays a calendar
-->
カレンダーを表示

    $ cal 12 1984

<!--
What day is today?
-->
今日はどんな日か調べる

    $ cal | sed "s/.*/ & /;s/ $(date +%d) / [] /"
    $ cal | sed "s/.*/ & /;s/ $(date +%d) / $(printf '\e[0;31m[]\e[0m') /"

<!--
What date was it yesterday or will it be tomorrow, etc...
-->
昨日はどんな日だったか、明日はどんな日か、など

    $ date -d yesterday
    $ date -d tomorrow +%Y-%m-%d
    $ date -d "7 days ago" +%Y-%m-%d
    $ date -j -v-1d (BSD)

<!--
Show File System Hierarchy
-->
ファイルシステム階層 (FHS) を表示

    $ man hier

<!--
Quick access to the ascii table
-->
手早くアスキーコード一覧を表示

    $ man ascii

<!--
Shutdown the system at a given time
-->
指定した時間にシャットダウンする

    $ shutdown -h now
    $ shutdown -h 22:49

<!--
Russian Roulette in Bash
-->
Bash によるロシアンルーレット

    $ [ $[ $RANDOM % 6 ] == 0 ] && echo "You die" || echo "You live"

<!--
Watch Star Wars via telnet
-->
Telnet 経由でスターウォーズを観る

    $ telnet towel.blinkenlights.nl


[command line one-liners]: http://arturoherrero.com/2013/11/29/command-line-one-liners/
