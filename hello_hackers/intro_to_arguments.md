# Intro to Arguments

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
