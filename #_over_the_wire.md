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

