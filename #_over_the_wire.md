# Over the Wire

## Bandit Level 0

In this challenge, we need to log into the game using `ssh`.
- Host : `bandit.labs.overthewire.org`
- Port : `2220` (use argument `-p` to pass the port)
- Username : `bandit0`

Command used : `ssh bandit0@bandit.labs.overthewire.org -p 2220`

Running this the host server will ask the password.
- Password : `bandit0`

## Bandit Level 0 → Level 1

Instruction : The password for the next level is stored in a file called `readme`, 
located in the home directory.

Command used : `cat readme`

This returns : <br>
`The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

Run `exit` to exit level 0.

Each time to log into the next level use : <br>
`ssh bandit[level_number]@bandit.labs.overthewire.org -p 2220`

Enter the password `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`.

## Bandit Level 1 → Level 2

Instruction : The password for the next level is stored in a file called `-`, 
located in the home directory.
<br>
Command used : `cat ./-`
<br>
This returns : `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`,
which is the password for the next level, so you can `exit`.
<br>
Log in into level 3 and continue.

## Bandit Level 2 → Level 3

Instruction : The password for the next level is stored in a file called "spaces in this filename" 
located in the home directory.
<br>
This returns : `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`, 
which is the password for the next level, so you can `exit`.
<br>
Log in into level 3 and continue.

## Bandit Level 3 → Level 4

Instruction : The password for the next level is stored in a hidden file in the `inhere` directory.

```
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
```

This returns : `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`,
which is the password for the next level, so you can `exit`.
<br>
Log in into level 4 and continue.

## Bandit Level 4 → Level 5

Instruction : The password for the next level is stored in the only human-readable file in the `inhere` directory.

```
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ file ./-file0*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
```

This returns : `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`,
which is the password for the next level, so you can `exit`.
<br>
Log in into level 5 and continue.

## Bandit Level 5 → Level 6

Instructions : The password for the next level is stored in a file somewhere under the `inhere` directory, 
and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

```
bandit5@bandit:~$ find -size 1033c
./inhere/maybehere07/.file2
bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
```

(Here,  I just checked for a file of size 1033 and got lucky.)
<br>
This returns : `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`,
which is the password for the next level, so you can `exit`.
<br>
Log in into level 6 and continue.

## Bandit Level 6 → Level 7

Instructions : The password for the next level is stored somewhere on the server, 
and has all of the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

```
bandit6@bandit:~$ cd /
bandit6@bandit:/$ find -type f -size 33c -group bandit6 -user bandit7 2> /dev/null
./var/lib/dpkg/info/bandit7.password
bandit6@bandit:/$ cat ./var/lib/dpkg/info/bandit7.password
```

Firstly, `cd` to the root directory to search the full server. 
Then I passed all the required arguments to the `find` function. 
However, this initially returns all the files we don't have permission to acces. 
So we use piping `2>` to append the error-free result to `/dev/null`. 
<br>
This returns : `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`
which is the password for the next level, so you can `exit`.
<br>
Log in into level 7 and continue.

## Bandit Level 7 → Level 8

Instructions : The password for the next level is stored in the file `data.txt`, 
next to the word `millionth`.

```
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
where, `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc` is the password, so you can exit.
<br>
I assumed `data.txt` would have a dump of data so I used `grep` to find `millionth`.
I piped the output of `cat` as the input of `grep` using `|`.
<br>
Log into level 8 and continue.

## Bandit Level 8 → Level 9

Instructions : 

```
bandit8@bandit:~$ cat data.txt | sort | uniq -u
```

This returns : `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM` 
which is the password for the next level, so you can `exit`.
<br>
Log in into level 9 and continue.

