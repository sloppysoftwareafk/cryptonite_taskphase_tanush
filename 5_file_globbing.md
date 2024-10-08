# File Globbing

## Matching with *

When it encounters a * character in any argument, the shell will treat it as "wildcard" 
and try to replace that argument with any files that match the pattern.

```
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{cVVPTZBFW4ERIeugkhLvqjXxQ2-.dFjM4QDL0ITN0czW}
```

In this challenge, we need to `cd` to the `/challenge` directory.
The catch is you can only pass four characters as the argument to the command.

## Matching with ?

When it encounters a ? character in any argument, the shell will treat it as single-character wildcard.
This works like *, but only matches one character.

```
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{khY_doe1W_ooKct594If81TuL2V.dJjM4QDL0ITN0czW}
```

In this challenge, we need to `cd` to the `/challenge` directory.
The catch is you need to use `?` to glob `c` and `l` in the directory name.

## Matching with []

The square brackes are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n.

```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ ls
file_a  file_c  file_e  file_g  file_i  file_k  file_m  file_o  file_q  file_s  file_u  file_w  file_y
file_b  file_d  file_f  file_h  file_j  file_l  file_n  file_p  file_r  file_t  file_v  file_x  file_z
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{4m9ijsUTdeKhuL0jMlvhH8Ps49Q.dNjM4QDL0ITN0czW}
```

In this challenge, we need to `cd` to the `/challenge/files` directory.
The catch is you need to use `[]` to glob just the 
`file_b`, `file_a`, `file_s`, and `file_h` files, 
by passing file_[bash] as the argument.

## Matching paths with []

Globbing happens on a path basis, so you can expand entire paths with your globbed arguments.

```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{UEcgXR2-w0oM0ul44x3EzJeFCI3.dRjM4QDL0ITN0czW}
```

In this challenge, we need to use `[]` to glob just the 
`file_b`, `file_a`, `file_s`, and `file_h` files, 
by passing file_[bash] as the argument.
The catch is we can't `cd` to the directory.

## Mixing globs

Note : This took 30 minutes. -_-

```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      delightful   great       jovial    magical     pwning   splendid   victorious  youthful
beautiful    educational  happy       kind      nice        queenly  thrilling  wonderful   zesty
challenging  fantastic    incredible  laughing  optimistic  radiant  uplifting  xenial
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{0aCnosMVZDk9fW4HRqi0HKdP10y.dVjM4QDL0ITN0czW}
```

In this challenge, using the globbing we've learned, we had to write a single, short (6 characters or less) glob that will match the files "challenging", "educational", and "pwning" ... to retrieve the flag.

## Exclusionary Globbing

If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed.

```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{MIJwiabKQCZOyW4-Z1YgH3ajtW6.dZjM4QDL0ITN0czW}
```

In this challenge, we need to run the files without names satrting with {p,w,n}.
TO achieve this, we invert the globbing by using `!` as the first character in `[]`.