# Perceiving Permissions

## Changing File Ownership

`chown` command is used to change the ownership of the file.
<br>
Syntax : `chown [username] [file]`
<br>
Note : `chown` can only be invoked by the root user.

```
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{YBqIh0PrNcKKq9rP5vPqFJo9F_z.dFTM2QDL0ITN0czW}
```

In this challenge, we need to change the owner of the `/flag` file to the hacker user, 
then print its contents to retrieve the flag.

## Groups and Files

Files have both an owning user and group.
You can check what groups you are part of with the `id` command.
Group ownership can be changed with the `chgrp` (change group) command. 
Unless you have write access to the file and membership in the new group, 
this typically requires root access.

```
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{gsuVZCbpzWn2QUzv-irSZxFNqiy.dFzNyUDL0ITN0czW}
```

In this challenge we need to change the group of `/flag` to `hacker` owned from `root`.
Then read it to retrieve the flag.

## Fun with Groups Names

In this challenge, we have to `chgrp` of `/flag` to the group hacker is in.
The catch is the group name is randomised.
Find the group `chgrp` to it and read the flag.

```
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp30386) groups=1000(grp30386)
hacker@permissions~fun-with-groups-names:~$ chgrp grp30386 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{8XdNn1rGxYNL4LQA1XfYl7iAwE5.dJzNyUDL0ITN0czW}
```

## Changing Permissions

