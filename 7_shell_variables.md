# Shell Variables

## Printing Variables

We already learnt that the `echo` command "echoes", that is, 
prints the arguments passed to it.
<br>
Things we learnt : It can also print out the values of variables.
<br>
This is done by prepending the variable names with a `$`.

```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{8TPD3b6RFiQWyBZIyOUbBuEcYXi.ddTN1QDL0ITN0czW}
```

In this challenge,  we had to print the value of the variable named `FLAG`.
The variable contains the flag.

## Setting Variables

Naturally, as well as reading values stored in variables, you can write values to variables.
This is done, as with many other languages, using `=`.
<br>
Note : There are no spaces around the `=`.
If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment.
It will instead, try to run the `VAR` command (which does not exist).
<br>
Note : The `$` is only prepended to access variables.
In shell terms, this prepending of $ triggers what is called variable expansion, and is, 
surprisingly, the source of many potential vulnerabilities.

```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{cZxj7cNPHw0kXT3vdlQ1UR62LYO.dlTN1QDL0ITN0czW}
```

In this challenge, we need to set the `PWN` variable to the value `COLLEGE`.
This retrieves the flag.

## Multi-word Variables

Note : Spaces have special significance in the shell, 
and there are places where you can't use them spuriously.
<br>
When the shell sees a space, it ends the variable assignment and interprets the next word as a command.
To bypass this, you need to quote the parameter.

```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{cPQC7old3ULU_FClE93Vk1-tEbZ.dBjN1QDL0ITN0czW}
```

In this challenge, we need to set the variable `PWN` to `COLLEGE YEAH` to retrieve the flag.

## Exporting Variables

By default, variables that you set in a shell session are local to that shell process.
That is, other commands you run won't inherit them.
<br>
Things we learnt : The `$` prompt is the prompt of `sh`, 
a minimal shell implementation that invoked as a child of the main shell process. 
And it does not receive the local variable.
<br>
When you `export` your variables, they are passed into the environment variables of child processes.

```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great
job! Here is your flag:
pwn.college{EYYVOk7DUTKN2C5kUBWYZioucdZ.dJjN1QDL0ITN0czW}
```

In this challenge, you must invoke `/challenge/run` with the `PWN` variable exported, 
and set to the value `COLLEGE`, and the `COLLEGE` variable set to the value `PWN`, 
but not exported (e.g., not inherited by `/challenge/run`) to retrieve the flag.

## Printing Exported Variables

Things we learnt : The `env` command prints out every exported variable set in your shell.

```
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
DOJO_AUTH_TOKEN=687d30ae5e83126e796fefc9859730045520b217528b1dc208f07e3b660e5713
HOME=/home/hacker
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.7z=01;31:*.ace=01;31:*.alz=01;31:*.apk=01;31:*.arc=01;31:*.arj=01;31:*.bz=01;31:*.bz2=01;31:*.cab=01;31:*.cpio=01;31:*.crate=01;31:*.deb=01;31:*.drpm=01;31:*.dwm=01;31:*.dz=01;31:*.ear=01;31:*.egg=01;31:*.esd=01;31:*.gz=01;31:*.jar=01;31:*.lha=01;31:*.lrz=01;31:*.lz=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.lzo=01;31:*.pyz=01;31:*.rar=01;31:*.rpm=01;31:*.rz=01;31:*.sar=01;31:*.swm=01;31:*.t7z=01;31:*.tar=01;31:*.taz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tgz=01;31:*.tlz=01;31:*.txz=01;31:*.tz=01;31:*.tzo=01;31:*.tzst=01;31:*.udeb=01;31:*.war=01;31:*.whl=01;31:*.wim=01;31:*.xz=01;31:*.z=01;31:*.zip=01;31:*.zoo=01;31:*.zst=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
FLAG=pwn.college{sTvLFGDYyJx6EZWudNvycEYcB2a.dhTN1QDL0ITN0czW}
LESSCLOSE=/usr/bin/lesspipe %s %s
TERM=xterm
LESSOPEN=| /usr/bin/lesspipe %s
SHLVL=1
LC_CTYPE=C.UTF-8
PATH=/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
_=/run/workspace/bin/env
```

IN this challenge, we need to look through all the exported variables, 
and find the value of the `FLAG` variable.

## Storing command output

Command Substitution is storing the output of some command into a variable.
<br>
Syntax : `FLAG=$(cat /flag)`

```
hacker@variables~storing-command-output:~$ PWN=`/challenge/run`
Congratulations! You have read the flag into the PWN variable. Now print it out
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN
pwn.college{s2AheWzdO6ITgTbp1qMGvhuco_v.dVzN0UDL0ITN0czW}
```

In this challenge,  we need to store the output of `/challenge/run` in `PWN` variable.
Print the value of the variable to retrieve the flag.

## Reading Input

The `read` built-in command is used to read input.
<br>
Things we learnt : The `-p` argument lets you specify a prompt.
<br>
Note : `read` reads data from your standard input.

```
hacker@variables~reading-input:~$ read -p "PWN = " PWN
PWN = COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{EQB_6M0h83w_Y_Gy2_loMekZQTR.dhzN1QDL0ITN0czW}
```

## Reading Files

Piping `<` can be used to redirect the contents of a file to a variable.
Obviously this enlists the help of the `read` command.

```
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{IDIoGV7xYT8lGpen6NQi7AgU1x9.dBjM4QDL0ITN0czW}
```

In this challenge, we need to "read" `/challenge/read_me` into the `PWN` environment variable, 
to retrieve the flag.
But the catch is we can only use one command line, 
as the value of `/challenge/read_me` keeps changing.