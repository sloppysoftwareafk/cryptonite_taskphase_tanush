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

