# Hello Hackers

## Intro to Commands

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

## Intro to Arguments

Arguments are what we call additional data passed to the command.
When you type a line of text and hit enter, the shell actually parses your input into a command and its arguments.
The first word is the command, and the subsequent words are arguments.

```
hacker@hello~intro-to-arguments:~$ echo hello
hello
hacker@hello~intro-to-arguments:~$ echo hello hackers
hello hackers
```

In the above example, `echo` is the command and `hello` and `hello` are the arguments.
`echo` is a simple command that "echoes" all of its arguments back out onto the terminal.

```
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{ARcXeDte3zXP1ihgjgVWrGENfhu.dhjNyUDL0ITN0czW}
```

In this challenge we learnt how to pass arguments to a command, and used the `echo` and `hello` commands.
The main challenge in the exercise is to obtain the flag from the terminal by invoking `hello` and pass the argument `hackers`, which gives a message of success and prints the flag.
This flag is then pasted to the `pwn.college` challenge box to signify the task is done.
