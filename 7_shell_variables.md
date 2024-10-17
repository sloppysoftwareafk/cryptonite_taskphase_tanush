# Shell Variables

## Printing Variables

We already learnt that the `echo` command "echoes", that is, 
prints the arguments passed to it.
<br>
Things we learnt : It can also print out the values of variables.
<br>
This is done by prepending the variable names with a `$`.

```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{8TPD3b6RFiQWyBZIyOUbBuEcYXi.ddTN1QDL0ITN0czW}
```

In this challenge,  we had to print the value of the variable named `FLAG`.
The variable contains the flag.

## Setting Variables

Naturally, as well as reading values stored in variables, you can write values to variables.
This is done, as with many other languages, using `=`.
<br>
Note : There are no spaces around the `=`.
If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment.
It will instead, try to run the `VAR` command (which does not exist).
<br>
Note : The `$` is only prepended to access variables.
In shell terms, this prepending of $ triggers what is called variable expansion, and is, 
surprisingly, the source of many potential vulnerabilities.

```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{cZxj7cNPHw0kXT3vdlQ1UR62LYO.dlTN1QDL0ITN0czW}
```

In this challenge, we need to set the `PWN` variable to the value `COLLEGE`.
This retrieves the flag.

## Multi-word Variables

Note : Spaces have special significance in the shell, 
and there are places where you can't use them spuriously.
<br>
When the shell sees a space, it ends the variable assignment and interprets the next word as a command.
To bypass this, you need to quote the parameter.

```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{cPQC7old3ULU_FClE93Vk1-tEbZ.dBjN1QDL0ITN0czW}
```

In this challenge, we need to set the variable `PWN` to `COLLEGE YEAH` to retrieve the flag.

## Exporting Variables

By default, variables that you set in a shell session are local to that shell process.
That is, other commands you run won't inherit them.
<br>
Things we learnt : The `$` prompt is the prompt of `sh`, 
a minimal shell implementation that invoked as a child of the main shell process. 
And it does not receive the local variable.
<br>
When you `export` your variables, they are passed into the environment variables of child processes.

```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great
job! Here is your flag:
pwn.college{EYYVOk7DUTKN2C5kUBWYZioucdZ.dJjN1QDL0ITN0czW}
```

In this challenge, you must invoke `/challenge/run` with the `PWN` variable exported, 
and set to the value `COLLEGE`, and the `COLLEGE` variable set to the value `PWN`, 
but not exported (e.g., not inherited by `/challenge/run`) to retrieve the flag.