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

Always remember : <br>
The first character there is the file type. 
The next nine characters are the actual access permissions of the file or directory, 
split into 3 characters denoting permissions for the owning user, 
3 characters denoting the permissions for the owning group, 
and 3 characters denoting the permissions that all other access has to the file.
<br>
Each character of the three represent permission for a different type:
- `r` - user/group/other can read the file (or list the directory)
- `w` - user/group/other can modify the files (or create/delete files in the directory)
- `x` - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
- `-` - nothing
<br>
Modifying an existing mode. 
`chmod` allows you to tweak permissions with the mode format of WHO+/-WHAT, 
where WHO is user/group/other and WHAT is read/write/execute. 
For example, to add read access for the owning user, you would specify a mode of u+r. 
Write and execute access for the group and the other (or all the modes) are specified the same way. 
More examples:
- u+r, as above, adds read access to the user's permissions
- g+wx adds write and execute access to the group's permissions
- o-w removes write access for other users
- a-rwx removes all permissions for the user, group, and world

```
hacker@permissions~changing-permissions:~$ chmod a+r /flag
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{UHl9F9ixllbF3HmTpM05Z9fpLQL.dNzNyUDL0ITN0czW}
```

In this challenge, we had to modify the permissions of `/flag`. 
To make it readable to the user, we use `u+r` with `chmod`.
Read the file to retrieve the flag.

## Executable Files



```
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-- 1 hacker hacker 32 Jul  4 06:37 /challenge/run
hacker@permissions~executable-files:~$ chmod a+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{oF9jYZm33EET9FHA_-IMhbyFZnS.dJTM2QDL0ITN0czW}
```