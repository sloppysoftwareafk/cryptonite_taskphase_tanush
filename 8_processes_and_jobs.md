# Processes and Jobs

## Listing processes

We can list running processes using the `ps` command.
`ps` either stands for "process snapshot" or "process status", and it lists processes.
<br>
Standard" Syntax: You can use `-e` to list every process and `-f` for a full format output, including arguments. These can be combined into a single argument `-ef`.
<br>
BSD Syntax: In this syntax, you can use `a` to list processes for all users,`x` to list processes that aren't running in a terminal, and `u` for a "user-readable" output. These can be combined into a single argument `aux`.

```
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 13:42 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-init /run/dojo/bin/sl
root           7       1  0 13:42 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 13:42 ?        00:00:00 /challenge/15201-run-839
root          72      68  0 13:42 ?        00:00:00 sleep 6h
hacker        73       0  0 13:42 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        90      73  0 13:43 pts/0    00:00:00 ps -ef
hacker@processes~listing-processes:~$ /challenge/15201-run-839
Yahaha, you found me! Here is your flag:
pwn.college{M0fvPw4dZzENz3bsgH--5B7GfPI.dhzM4QDL0ITN0czW}
Now I will sleep for a while (so that you could find me with 'ps').
```

In this challennge, we had to look thru all the running processes.
After finding the renamed `/challenge/run` here, `/challenge/15201-run-839`, 
run it to retrieve the flag.

## Killing Processes

```
hacker@processes~killing-processes:~$ ps -ef | grep dont_run
hacker        73      71  0 13:52 ?        00:00:00 /challenge/dont_run
hacker       114      92  0 13:53 pts/1    00:00:00 grep --color=auto dont_run
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{gidhbo60F2oD_jPQXSiUsu29t__.dJDN4QDL0ITN0czW}
```

In this challenge, we had to find the `/challenge/dont_run` process.
After finding it, `kill` it using its `PID` here, 73 and then...
`/challenge/run` to retrieve the flag.

## Interrupting Processes

The hotkey : `Ctrl-C` (e.g., holding down the `Ctrl` key and pressing `C`) 
sends an "interrupt" to whatever application is waiting on input from the terminal and, 
typically, this causes the application to cleanly exit.
<br>
It helps to get rid of the process that's clogging up your terminal.

```
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{g8swVSfpbDdzt7aMtjllAYJ2Tx7.dNDN4QDL0ITN0czW}
```

In this challenge, we need to run the `/challenge/run` process and then interrupt it, 
to retrieve the flag.

## Suspending Processes

Things we learnt : You can suspend processes to the background with `Ctrl-Z`.

```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         100      82  0 16:45 pts/1    00:00:00 bash /challenge/run
root         102     100  0 16:45 pts/1    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         100      82  0 16:45 pts/1    00:00:00 bash /challenge/run
root         107      82  0 16:45 pts/1    00:00:00 bash /challenge/run
root         109     107  0 16:45 pts/1    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{40I4wEVMfAD2JFe79Gu76l20MpT.dVDN4QDL0ITN0czW}
```

In this challenge, run, that is, `/challenge/run` wants to see another copy of itself running 
and using the same terminal. 
Use the terminal to launch it, then suspend it, 
then launch another copy while the first is suspended to retrieve the flag.

## Resuming Processes

VERY IMPORTANT : `ps -o user,pid,stat,cmd`
<br>
This shows the running status of all the processes.
<br>

To resume processes, your shell provides the fg command, 
a builtin that takes the suspended process, resumes it, 
and puts it back in the foreground of your terminal.

```
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{EGpDEp5HViaRYjDKx4TnpYug32q.dZDN4QDL0ITN0czW}
Don't forget to press Enter to quit me!
^C
hacker@processes~resuming-processes:~$
```

In this challengem, `/cahllenge/run` needs you to suspend it, then resume it.
This returns the flag.

## Backgrounding Processes

The `bg` command : This will allow the process to keep running, 
while giving you your shell back to invoke more commands in the meantime.
<br>
Note : The `fg` command resumes the process in the foreground.

```
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          99 S+   bash /challenge/run
root         101 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          99 S    bash /challenge/run
root         109 S    sleep 6h
root         110 S+   bash /challenge/run
root         112 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{UX7AyiWk0V0IlNUXq1k-K7NsLKD.ddDN4QDL0ITN0czW}
```

## Foregrounding Processes

You can foreground a backgrounded process with `fg` just like you foreground a suspended process.

```
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &



Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.
hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{YUTdzTfR8DR-wemUsNLH4AZXOsr.dhDN4QDL0ITN0czW}
```

In this challenge, we need to run `/challenge/run`, then suspend it, 
then resume it in `bg` and then push it to `fg` to retrieve the flag.

## Starting Bachground Processes

You can start the process backgrounded right off the bat, 
all you have to do is append a `&` to the command.

```

In this challenge, we need to start `/challenge/run` directly in the background.
This returns the flag.

## Process Exit Codes

