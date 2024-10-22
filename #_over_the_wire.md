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

