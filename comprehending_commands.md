# COmprehending Commands

## cat : not the pet, but the command

One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files.
`cat` will concatenate (hence the name) multiple files if provided multiple arguments.
<br>
In this challenge, the flag is stored in the `flag` path in the home directory.
Calling that path, will return the flag.

```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{443QBO0J7D_48D_0bVHGBFcgzPh.dFzN1QDL0ITN0czW}
```

Note: If you give no arguments at all, cat will read from the terminal input and output it.

## catting absolute paths

Unlike the last challenge, in this one the flag is stored in the absolute path `/flag`.
Calling that path, will return the flag.

```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{E5OzBlemBzax2FpfoQwcQz70moD.dlTM5QDL0ITN0czW}
```

Fun fact : `/flag` is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

## More catting practice

In this challenge, we must retrieve the flag by using the absolute path of the directory as an argument to `cat`.

```You cannot use the 'cd' command in this level, and must retrieve the flag by
absolute path. Plus, I hid the flag in a different directory! You can find it
in the file /usr/lib/tcltk/flag. Go cat it out **without** cding into that
directory!
hacker@commands~more-catting-practice:~$ cat /usr/lib/tcltk/flag
pwn.college{wxniAps88fmhGT70-PXNReP_21T.dBjM5QDL0ITN0czW}
```

Things we learnt : You can specify all sorts of paths as arguments to commands.

## Grepping for a needle in a haystack

Sometimes, the files that you might cat out are too big.
The grep command to search for the contents we need.
<br>
Syntax : `hacker@dojo:~$ grep SEARCH_STRING /path/to/file`
<br>
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{oPiZozby9PIL17Koth-Jt7fn_Of.ddTM4QDL0ITN0czW}
```

In this challenge, we use the `grep` command to search for the flag in the hundreds of lines of text.
Hint : The flag always contains the string `pwn.college`.

## Listing files

`ls` will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided.
In this challenge we need to access the path of the directory by running the path containing the flag after finding it in the listed files under the `/challenge` directory.

```
hacker@commands~listing-files:~$ ls /challenge
596-renamed-run-1628  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/596-renamed-run-1628
Yahaha, you found me! Here is your flag:
pwn.college{gYPUZm3PMeVJq3vgfybWxsNAF9d.dhjM4QDL0ITN0czW}
```

## Touching files

You can create a new, blank file by *touching* it with the `touch` command.

```
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{8Wn2qWADpec9hY06U-24JuVWVgQ.dBzM4QDL0ITN0czW}
```

In this challenge, we need to create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get the flag.

## Removing files

In Linux, you remove files with the `rm` command.

```
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{Q8dvEc70vYNrhUaOJoqAr11lUZk.dZTOwUDL0ITN0czW}
```

In this challenge, we need to delete the `delete_me` file in the home directory.
And then run `/challenge/check`, which will check the deletion.
If removed successfully it will return the flag.

## Hidden files

`ls` doesn't list all the files by default.
Linux has a convention where files that start with a `.` don't show up by default in `ls` and in a few other contexts.
To view them with `ls`, you need to invoke `ls` with the `-a` flag.

```
hacker@commands~hidden-files:~$ ls
'~'
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls
bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv            bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-89832696815191  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:~$ cat /.flag-89832696815191
pwn.college{QF2qaS6IrjVnY18fGEbktohshrB.dBTN4QDL0ITN0czW}
```

In this challenge, we had to find the flag in a dot prepended hidden file in a file in the `/` directory.

## An Epic Filesystem Quest

In this challenge, the hidden flag has to be retrieved through following the breadcrumbs.
Using the `cd`, `ls` and `cat` functions.

```
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
POINTER  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin      challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat POINTER
Congratulations, you found the clue!
The next clue is in: /usr/local/lib/python3.8/dist-packages/pwn/__pycache__

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/$ ls /usr/local/lib/python3.8/dist-packages/pwn/__pycache__
INFO-TRAPPED  __init__.cpython-38.pyc  toplevel.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/$ cat /usr/local/lib/python3.8/dist-packages/pwn/__pycache__/INFO-TRAPPED
Tubular find!
The next clue is in: /usr/share/racket/pkgs/scribble-lib/scribble/elsarticle

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/share/racket/pkgs/scribble-lib/scribble/elsarticle
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/elsarticle$ ls
HINT  compiled  elsarticle.tex  lang  lang.rkt  style.tex
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/elsarticle$ cat HINT
Tubular find!
The next clue is in: /usr/share/racket/pkgs/scribble-lib/scribble/book/lang
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/elsarticle$ cd /usr/share/racket/pkgs/scribble-lib/scribble/book/lang
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/book/lang$ ls
CUE  compiled  reader.rkt
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/book/lang$ cat CUE
Lucky listing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/pip/_internal/operations

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/book/lang$ cd /usr/local/lib/python3.8/dist-packages/pip/_internal/operations
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/pip/_internal/operations$ ls
BLUEPRINT  __init__.py  __pycache__  build  check.py  freeze.py  install  prepare.py
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/pip/_internal/operations$ cat BLUEPRINT
Lucky listing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/debugpy-1.8.5.dist-info

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/pip/_internal/operations$ cd /usr/local/lib/python3.8/dist-packages/debugpy-1.8.5.dist-info
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/debugpy-1.8.5.dist-info$ ls
INSTALLER  LICENSE  METADATA  README  RECORD  WHEEL  entry_points.txt  top_level.txt
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/debugpy-1.8.5.dist-info$ cat README
Tubular find!
The next clue is in: /opt/busybox/busybox-1.33.2/include/config/feature/tar/long

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/debugpy-1.8.5.dist-info$ cd /opt/busybox/busybox-1.33.2/include/config/feature/tar/long
hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/include/config/feature/tar/long$ ls
MEMO  options.h
hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/include/config/feature/tar/long$ cat MEMO
Lucky listing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/scapy/contrib
hacker@commands~an-epic-filesystem-quest:/opt/busybox/busybox-1.33.2/include/config/feature/tar/long$ cd /usr/local/lib/python3.8/dist-packages/scapy/contrib
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/scapy/contrib$ ls
REVELATION               cdp.py                    gtp.py              isotp           nfs.py          portmap.py      sebek.py
__init__.py              chdlc.py                  gtp_v2.py           knx.py          nlm.py          postgres.py     send.py
__pycache__              coap.py                   gxrp.py             lacp.py         nrf_sniffer.py  ppi_cace.py     skinny.py
altbeacon.py             concox.py                 hicp.py             ldp.py          nsh.py          ppi_geotag.py   slowprot.py
aoe.py                   diameter.py               homeplugav.py       lldp.py         oam.py          ripng.py        socks.py
automotive               dtp.py                    homepluggp.py       loraphy2wan.py  oncrpc.py       roce.py         stamp.py
avs.py                   eddystone.py              homeplugsg.py       ltp.py          opc_da.py       rpl.py          stun.py
bfd.py                   eigrp.py                  http2.py            mac_control.py  openflow.py     rpl_metrics.py  tacacs.py
bgp.py                   enipTCP.py                ibeacon.py          macsec.py       openflow3.py    rsvp.py         tcpao.py
bier.py                  erspan.py                 icmp_extensions.py  metawatch.py    ospf.py         rtcp.py         tcpros.py
bp.py                    esmc.py                   ife.py              modbus.py       pfcp.py         rtps            tzsp.py
cansocket.py             ethercat.py               igmp.py             mount.py        pim.py          rtr.py          vqp.py
cansocket_native.py      etherip.py                igmpv3.py           mpls.py         pnio.py         rtsp.py         vtp.py
cansocket_python_can.py  exposure_notification.py  ikev2.py            mqtt.py         pnio_dcp.py     scada           wireguard.py
carp.py                  geneve.py                 isis.py             mqttsn.py       pnio_rpc.py     sdnv.py
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/scapy/contrib$ cat REVELATION
Lucky listing!
The next clue is in: /usr/share/doc/libgit2-28

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/scapy/contrib$ cd /usr/share/doc/libgit2-28
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgit2-28$ ls
changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgit2-28$ ls -a
.  ..  .EVIDENCE  changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libgit2-28$ cat .EVIDENCE
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{An9ICHGWvMVe4_jUCz9HkQ6H99t.dljM4QDL0ITN0czW}
```

## Making directories

Things we learnt : We can create directories using the `mkdir` command.
It uses the absolute path as its parameter.


```
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ cd /tmp/pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ cd
hacker@commands~making-directories:~$ /challenge/run
Success! Here is your flag:
pwn.college{Uh1DGYuxJQM_uI_fq1bb8G3SSKb.dFzM4QDL0ITN0czW}
```

In this challenge, we need to `touch` the `college` file in the newly created `/tmp/pwn` directory.
Using `mkdir` command, and then running `/challenge/run` to retrieve the flag.

## Finding files

The `find` command takes optional arguments describing the search criteria and the search location.
If you don't specify a search criteria, `find` matches every file.
If you don't specify a search location, `find` uses the current working directory (.).
<br>
In this challenge, we need to find a file named `flag` which contains the flag.
Since multiple like named files exist, read them all using `cat` until you retrieve the flag.

```
hacker@commands~finding-files:~$ find / -name flag
find: ‘/tmp/tmp.MiOQGWw5Zc’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/local/share/radare2/5.9.5/flag
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/root’: Permission denied
/opt/aflplusplus/.git/hooks/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/opt/radare2/libr/flag
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cat /usr/local/share/radare2/5.9.5/flag
cat: /usr/local/share/radare2/5.9.5/flag: Is a directory
hacker@commands~finding-files:~$ cat /opt/aflplusplus/.git/hooks/flag
pwn.college{0h44aTUIuh1HwtEe9TgAbEc_y0i.dJzM4QDL0ITN0czW}
```

Things we learnt : Syntax = `find / -name <file_name>`.
It searches the whole filesystem for the file named `<file_name>`.

## Linking files

Things we learnt : Symbolic links (also also known as symlinks) are created with the `ln` command with the `-s` argument.
<br>
Note : The original file path comes *before* the link path in the command!
<br>
Fun Fact : A symlink can be identified as such with a few methods. For example, the file command, which takes a filename and tells you what type of file it is.

```
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
cat: /home/hacker/not-the-flag: No such file or directory
hacker@commands~linking-files:~$ ln -s /flag ~/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{k3sFvmbWYlXIo2FloAXzZydjH4Z.dlTM1UDL0ITN0czW}
```

In this challenge, we had to link the contents of `flag` to `~/not-the-flag`.
Since `/challenge/catflag` reads the contents of `~/not-the-flag`,
it will actually read the linked contents of `/flag`.  
