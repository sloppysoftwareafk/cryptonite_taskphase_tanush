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

## Killing Processes

