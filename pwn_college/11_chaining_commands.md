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

In this challenge, we had to had to write the chained command into a shell script.
The run the file as an argument to `bash` to retrieve the flag.

## Redirecting Script Output

As far as the shell is concerned, your script is just another command. 
That means you can redirect its input and output just like you did for commands in the Piping module.
<br>
All of the various redirection methods work: 
- `>` for stdout, 
- `2>` for stderr, 
- `<` for stdin, 
- `>>` and 2>> for append-mode redirection, 
- `>&` for redirecting to other file descriptors, 
- and `|` for piping to another command.

```
hacker@chaining~redirecting-script-output:~$ touch x.sh
hacker@chaining~redirecting-script-output:~$ echo "/challenge/pwn; /challenge/college" > x.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh > /challenge/solve
No shenanigans with bash options yet, please! Just run your script with 'bash
x.sh'.
ssh-entrypoint: /challenge/solve: Permission denied
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{wuAYigt0sO1sWoQ01RuQYyNUE5N.dhTM5QDL0ITN0czW}
```

This challenge is just like the previous one...
but the catch is we need to pipe `|` from our shell script to `/challenge/solve`.
This will return the flag.

## Executable Shell Scripts

Note : When you invoke bash script.sh, you are, 
of course launching the bash command with the script.sh argument. 
This tells bash to read its commands from script.sh instead of standard input, 
and thus your shell script is executed.
<br>
It turns out that you can avoid the need to manually invoke bash. 
If your shell script file is "executable", you can simply invoke it via its relative or absolute path.
<br>
In this challenge, we need to add `/challenge/solve` to the script.
Then make the script executable using `chmod a+x`. 
Run the script in the directory of the file to return the flag.
(you can also use the absolute path of the shell script)

```
hacker@chaining~executable-shell-scripts:~$ touch x.sh
hacker@chaining~executable-shell-scripts:~$ echo "/challenge/solve" > x.sh
hacker@chaining~executable-shell-scripts:~$ chmod a+x x.sh
hacker@chaining~executable-shell-scripts:~$ ./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{oQCfj_tb9tBQ4bqQD4tOgSiVAXx.dRzNyUDL0ITN0czW}
```
