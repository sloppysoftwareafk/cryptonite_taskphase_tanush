# Chaining Commands

## Chaining with semi-colons

You can chain commands using the semi-colon `;`.
<br>
Basically, when you hit Enter, your shell executes your typed command and, 
after that command terminates, give you the prompt to input another command. 
The semicolon is analogous, 
just without the prompt and with you entering both commands before anything is executed.

```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{wI9_HmxAMQKiz0WXs9WP1HverC0.dVTN4QDL0ITN0czW}
```

## Your first shell script

As you combine more and more commands to achieve complex effects, 
the length of the combined prompt quickly gets really annoying to deal with. 
When this happens, you can put these commands in a file, called a shell script, 
and run them by executing the file.
<br>
We can create a shell script called `[file_name].sh` 
(by convention, shell scripts are frequently named with a ".sh" suffix)
<br>
And then we can execute by passing it as an argument to a new instance of our shell (bash). 
When a shell is invoked like this, rather than taking commands from the user, 
it reads commands from the file.

```
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ echo "/challenge/pwn; /challenge/college" > x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{0zaBwWUID33XallUolEvtFc8_Cb.dFzN4QDL0ITN0czW}
```