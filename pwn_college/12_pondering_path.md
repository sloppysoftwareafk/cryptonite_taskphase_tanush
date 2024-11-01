# Pondering Path

## The PATH variable

There is a special shell variable, called `PATH`, 
that stores a bunch of directory paths in which the shell will search for programs, 
corresponding to commands. (including built-ins) 
<br>
If you blank out the PATH variable, that is, 
without a "PATH", bash cannot find the built-in commands.

```
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{0oZfhjGzTWvCtRzD3TGr8cuHC2-.dZzNwUDL0ITN0czW}
```

In this challenge, we need to erase the path of the `rm` function.
This will prevent `/challenge/run` from removing the flag.
As it can't find the path to `rm`, it will return the flag.

## Setting PATH

By adding directories to or replacing directories in this list (value of the `PATH` variable), 
you can expose these programs to be launched using their bare name.

```
hacker@path~setting-path:~$ PATH=/challenge/more_commands
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{okzZOB0pH_HOpNRRPZLi-qJgYs1.dVzNyUDL0ITN0czW}
```

In this challenge, we need to run the `win` command by invoking its bare name.
Adding the directory path (here `/challenge/more_commands`), 
where the command is found to `PATH` and then run `/challenge/run`.
This will return the flag.

## Adding commands

This took a while...
<br>
In this challenge, we need to create the `win` command as a shell script.

```
hacker@path~adding-commands:~$ echo $PATH
/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~adding-commands:~$ PATH=/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/hacker
hacker@path~adding-commands:~$ touch win
hacker@path~adding-commands:~$ echo "chmod a+x win; cat /flag" > win
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{88xUqEt1T8DcdWPKr-bQigf3WU0.dZzNyUDL0ITN0czW}
```

NOTE : 
- To invoke it by its bare name, its directory must be in `PATH`.
- We need to overwrite `PATH` and keep all the original directories.
- `win` by default won't be executable, so chain `chmod` to win.
<br>
If all conditions met to access `/flag` then the flag will be returned.

## Hijacking Commands

The objective in this challenge is same as the first challenge in this module.
<br>
The catch is that `/challenge/run` is set to run the `rm` command.
This would result in the `/flag` getting removed.

```
hacker@path~hijacking-commands:~$ touch rm
hacker@path~hijacking-commands:~$ chmod a+rwx rm
hacker@path~hijacking-commands:~$ echo $PATH
/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~hijacking-commands:~$ PATH=/home/hacker:/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
pwn.college{EliE5yqRJzCh0LXSulbr1TvPVxs.ddzNyUDL0ITN0czW}
```

The hint is that `/challenge/run` is set to run any file that it can find named `rm`.
This means like the third challenge, we can create a new script named `rm`.
<br>
The method : 
- Firstly, change the permissions of the file to executable.
- Now at first I was appending the home directory to the PATH variable.
This was resulting in the shell first finding the original `rm` function.
The solution is simply to prepend the home directory.
- Run `/challenge/run` to retrieve the flag.
