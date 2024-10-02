# Intro to Commands

We start with a simple interaction with the terminal by asking it for our identity by invoking the command `whoami`, to which the terminal returns the value `hacker`.
When the command terminates, the shell once again displays the prompt, ready for the next command.

```
hacker@hello~intro-to-commands:~$ whoami
hacker
```

The main challenge in the exercise is to obtain the flag from the terminal by invoking `hello`, which gives a message of success and prints the flag.
This flag is then pasted to the `pwn.college` challenge box to signify the task is done.

```
sloppysoftwareafk@Tanush:~$ ssh -i ./key hacker@dojo.pwn.college
Connected!
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{IF7p-u-_f80eYn9fiH8FIpzmOYe.ddjNyUDL0ITN0czW}
```

Things we learnt : Linux commands are case-sensitive. `hello` is different from `HELLO`
