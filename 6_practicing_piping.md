# Practicing Piping

## Redirecting output

You can use the `>` character to redirect stdout to files.

```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{UMxqymeNOgrRMP4U0HCwnK7RTJd.dRjN1QDL0ITN0czW}
```

In this challenge, we need to redirect `PWN` to the file `COLLEGE` to retrieve the flag.

## Redirecting more output

Aside from redirecting the output of echo, you can, of course, redirect the output of any command.
<br>
In this level, /challenge/run will once more give you a flag, 
but only if you redirect its output to the file myflag.
Your flag will, of course, end up in the myflag file.

```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{MwXjUPEkcbl2bfhvTa6eSTKtMhZ.dVjN1QDL0ITN0czW}
```

Note : `/challenge/run` will still happily print to your terminal, despite you redirecting stdout.
That's because it communicates its instructions and feedback over standard error, 
and only prints the flag over standard out.

## Appending output

You can redirect input in append mode using `>>` instead of `>`.

```
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
hacker@piping~appending-output:~$ echo stdout >> /home/hacker/the-flag
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 |
\|/ This is the first half:
 v
pwn.college{Ao66AB6b0NnqF_LpdX2cAXYYESq.ddDM5QDL0ITN0czW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>)
rather than *append* mode (>>), and so the write of the second half to stdout
overwrote the initial write of the first half directly to the file. Try append
mode!
```

Note : If you properly redirect in append-mode, the second half will be appended to the first, 
but if you redirect in truncation mode (>), 
the second half will overwrite the first and you won't get the flag!

## Redirecting errors

A File Descriptor (FD) is a number the describes a communication channel in Linux.
- FD 0: Standard Input
- FD 1: Standard Output
- FD 2: Standard Error
When you redirect process communication, you do it by FD number, though some FD numbers are implicit.

```
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{Ifv0Ri3ugPkIFYNDvWQt8j5n9mb.ddjN1QDL0ITN0czW}
```

In this challenge, you will need to redirect the output of /challenge/run, like before, to `myflag`, 
and the "errors" (in our case, the instructions) to `instructions`.
To retrieve the flag, read the `myflag` file.

## Redirecting input

Just like you can redirect output from programs, you can redirect input to programs.
This is done using `<`.

```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{skev5Q5MBWIDhRD8uDuuBSMoHil.dBzN1QDL0ITN0czW}
```

In this challenge, we will practice using `/challenge/run`, 
which will require you to redirect the `PWN` file to it and have the `PWN` file contain the value `COLLEGE`.
To write that value to the `PWN` file, recall the prior challenge on output redirection from echo.

## Grepping stored results

In this challenge, we need to : 
1. Redirect the output of /challenge/run to /tmp/data.txt.
2. This will result in a hundred thousand lines of text, 
with one of them being the flag, in /tmp/data.txt.
3. Grep that for the flag.

```
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{QmM1-Rr-THZkGeK9M6g6hlH3e5D.dhTM4QDL0ITN0czW}
```

## Grepping live output

the `|` (pipe) operator : Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe.

```
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
pwn.college{Eew0JrhAX1vahTYZoc47Uskkv2s.dlTM4QDL0ITN0czW}
```

In this challenge, `/challenge/run` will output a hundred thousand lines of text, including the flag.
Grep for the flag!

## Grepping errors

The `|` operator redirects only standard output to another program, 
and there is no `2|` form of the operator.
It can only redirect standard output.
<br>
The shell has a `>&` operator, which redirects a file descriptor to another file descriptor.
This means that we can have a two-step process to grep through errors: 
first, we redirect standard error to standard output `2>& 1` 
and then pipe the now-combined stderr and stdout as normal `|`.

```
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn.college
pwn.college{EJJ9hNNm-9aXTad3smT0UGHiVTV.dVDM5QDL0ITN0czW}
```

In this challenge, grep the standard error file to retrieve the flag.

## Duplicating piped data with tee

When you pipe data from one command to another, you of course no longer see it on your screen.
This is not always desired: for example,
you might want to see the data as it flows through between your commands to debug unintended outcomes.
<br>
The tee command, named after a "T-splitter" from plumbing pipes, 
duplicates data flowing through your pipes to any number of files provided on the command line.

```
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee myflag | /challenge/college
Processing...
WARNING: you are overwriting file myflag with tee's output...

The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat myflag
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "gsSzFWaT"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret gsSzFWaT | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{gsSzFWaTCZJR99HU0O_8TSMoUes.dFjM5QDL0ITN0czW}
```

In this challenge, this process' `/challenge/pwn` must be piped into `/challenge/college`, 
but you'll need to intercept the data to see what pwn needs from you.
<br>
You piped the output of `/challenge/pwn` to `/challenge/college` via tee `myflag`.
`tee` created `myflag` and wrote the output to both the file and `/challenge/college`. 
Error Message:<br>
`/challenge/college` complained about missing a secret code, hinting at using tee to intercept the output. 
Intercepting Output:<br>
You used cat `myflag` to reveal the program's usage information: /challenge/pwn requires a --secret flag followed by a specific secret code ("gsSzFWaT"). 
Solving the Challenge:<br>
You provided the correct secret code ("gsSzFWaT") using the `--secret` flag. This satisfied `/challenge/college` and resulted in a success message with your flag.

## Writing to multiple programs

Linux follows the philosophy that "everything is a file".
This is, the system strives to provide file-like access to most resources, including the input and output of running programs. 
The shell follows this philosophy, allowing you to, for example, 
use any utility that takes file arguments on the command line (such as `tee`) 
and hook it up to the input or output side of a program.
<br>
This is done using what's called Process Substitution. 
If you write an argument of `>(rev)`, bash will run the rev command 
(this command reads data from standard input, reverses its order, and writes it to standard output), 
but hook up its input to a temporary file that it will create. 
This isn't a real file, of course, it's what's called a named pipe.

```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack |tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{EkFlN0FQ8yPvHtMEk_fOTUE7vRo.dBDO0UDL0ITN0czW}
```

The command `>(/challenge/the)` creates a temporary named pipe and connects it to the standard input of `/challenge/the`. 
This allows you to treat the output of `/challenge/the` as if it were a file. 
The command tee reads the output of `/challenge/hack` and writes it to its standard output 
(which is the terminal) and to the temporary named pipe created in the previous step. 
The output of tee is then piped to `/challenge/planet`. 
This means that the output of `/challenge/hack` is now being sent to both `/challenge/the` and `/challenge/planet` simultaneously. 
Both /challenge/the and /challenge/planet will receive the output of `/challenge/hack` as their input and can process it accordingly.

## 

In this challenge, you have:
- `/challenge/hack` : this produces data on stdout and stderr
- `/challenge/the` : you must redirect hack's stderr to this program
- `/challenge/planet` : you must redirect hack's stdout to this program

```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) | /challenge/planet
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
pwn.college{8tkAzPSH6iPTB9EZwQcka3me0eq.dFDNwYDL0ITN0czW}
```