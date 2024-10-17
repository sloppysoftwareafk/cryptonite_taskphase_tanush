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