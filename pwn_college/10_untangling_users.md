# Untangling Users

## Becoming root with su

`su` (the Switch User command) : This is not typically used to elevate to root access anymore, 
but it is an elegant utility from a more civilized time, and we'll cover it first. 
<br>
`su` is a SUID binary.
Because it has the SUID bit set, su runs as root. 
Running as root, it can start a root shell. 
Of course, su is discerning: before allowing the user to elevate privileges to root, 
it checks to make sure that the user knows the root password.
<br>
This check against the root password is what obsoletes `su`.

```
hacker@users~becoming-root-with-su:~$ ls -l /usr/bin/su
-rwxr-xr-x 1 root root 67816 Apr  9  2024 /usr/bin/su
hacker@users~becoming-root-with-su:~$ su
Password:
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{Y-fp9BLDjMZpwTLKz1lnK-srf8L.dVTN0UDL0ITN0czW}
```

In this challenge, `su` has the root password `hack-the-planet`.
Run the root shell using the password and read the flag.

## Other users with su

Note : With no arguments, `su` will start a root shell (after authenticating with root's password).
<br>
However, you can also give a username as an argument to switch to that user instead of root.

```
hacker@users~other-users-with-su:~$ su zardus
Password:
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{Ep5JZnI81lOcjoe3TCrgj60LSsu.dZTN0UDL0ITN0czW}
```

In this challenge, we need to `su` to `zardus` and run `/challenge/run`.
This returns the flag.

## Cracking passwords

When you input a password into `su`, it one-way-encrypts (hashes) it, 
and compares the result against the stored value. 
If the result matches, `su` grants you access to the user.
<br>
Note : If you have the hashed value of the password, you can crack it.
<br>
If a hacker gets their hands on a leaked /etc/shadow, 
they can start cracking passwords and wreaking havoc. 
The cracking can be done via the famous John the Ripper.
<br>
Syntax : `john [file_name]`

```
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:09 93% 1/3 0g/s 283.8p/s 283.8c/s 283.8C/s zardus999992002..zardus1963
aardvark         (zardus)
1g 0:00:00:21 100% 2/3 0.04621g/s 269.0p/s 269.0c/s 269.0C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
hacker@users~cracking-passwords:~$ su zardus
Password:
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{oSQR8POqnTUmRRbJqDPiN8o7X2J.ddTN0UDL0ITN0czW}
```

In this challenge, we need to obtain the hashed password to `su` to `zardus`.
It turns out to be `aardvark` here. Enter it and `/challenge/run` to retrieve the flag.

## Using sudo

Unlike su, which defaults to launching a shell as a specified user, 
sudo defaults to running a command as root.

Also unlike su, rather than authenticating via password, 
sudo relies on policies that it checks to determine the user's authorization run things as root.

```
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{YUJUDiM8963PIJg7Y7Cu-wi6wVi.dhTN0UDL0ITN0czW}
```

In this challenge, we need to `sudo` to read the flag.
