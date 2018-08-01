## Legend
* **definition** - some important term or concept
* `command` - some important tool you need to know of
* `~/.filename` - some file you may know of (always path included)

To use `command` just run it. To locate it `which command`. To read manual (if avaialbe) `man command`. To find possible related documents about either definition/`command` try `apropos X`.

## Basics
* `access` - in order to change something you an access.
* `configuration` - you want your setup to persist in time on each boot.
* `session` - you want several typical layouts to work with something.
* `runtime`

## System toolbox
* `info` - what is it?
* `man` - manual page database
* `apropos name` - search for available man pages
* `~/.inputrc` - used by GNU readline library for advanced command line editing using keybindings, cursor movements, history, etc. The library is used by many common CLI tools: bash, more, etc. 

## Graphics/X11
* `~/.xinitrc`
* `~/.Xresources`

### Shell
* `interactive shell` - receive *user* commands, process it and gives the result.
* `system shell` - used silently to run system scripts where interaction with the user may not the case.
* `sh` - POSIX standard scripting language. Bash, zsh, dash, etc trying to suuport/comply to this standard. That simply means they can interpret .sh scripts.
* `in-band signaling` - shell uses inband signaling for both printing characters, change colors, move cursor, etc. The only shell make sense what to show and what to interpret as control signal.  
* `escape characters` - ... See https://en.wikipedia.org/wiki/ANSI_escape_code
* `terminal capabilities` 
    * list current capabilities `infocmp -c`
* `termcap database` 
    * readme `man terminfo`
    * list available `find /usr/share/terminfo -type f`
    * set (do not recommend) `export TERM = st-256colors`
* `fc` (fix command) - list/edit last typed command using `$VISUAL`/`$EDITOR`
* `tty` - print current TTY you attached to
* `stty -a` - look at the TTY device attached and show settings refer to UART parameters, some affect the line discipline and some are for job control all mixed up together
* `stty -F /dev/tty2 rows 5` - set terminal height to 5 lines
* `tput` - query capabilities of current terminal `$TERM` or reset/init it or query capabilities from terminfo database
* `shopt` - a shell builtin command to set and unset (remove) various Bash shell options 
* shell colors - ... Good brief on "Basic Color Terms: Their Universality and Evolution": https://stackoverflow.com/questions/4842424/list-of-ansi-color-escape-sequences#33206814. Good excerpt on Color partitioning (or how 256 posible terminal colors are formed and partitioned into groups): https://stackoverflow.com/questions/27159322/rgb-values-of-the-colors-in-the-ansi-extended-colors-index-17-255

### Shell history
Thomson shell -> PWB shell -> Borne shell (sh). Next see:

![shell history tree](https://www.ibm.com/developerworks/library/l-linux-shells/figure1.gif)

* Notes. <br>
`ksh, et al` takes best of `csh` and `bash`. `csh` is not recommended to use at all. `bash` is de-facto standard among Linux distributions. `zsh` is mainstream for "full-fledged" shell, the same with `fish` but it kinda more "underground". `mksh` is a default on Android. The performance is going as follows: `dash`, `mksh`, `zsh`, ... `bash`. Want to stay safe, minimal and authentic - go with `bash`. 

### How shell works
![shell boot process](https://www.ibm.com/developerworks/aix/library/au-getstartedbash/login2.gif)

### Unix history
Unix system created at AT&T Bell Labs. Written in C. It is "Self-contained" system. Lincences were sold to commercial companies IBM (AIX), Apple (OS X), HP (HP-UX), etc. Now is under jurisdiction of (maintained by) The Open Group. It's still alive (Solaris).

* `self-contained system` - system which has all the environment: compilers, debugers, documentations, etc.

Then, BSD appeared to substitute all the legal restrictions. Designed under Berkley University. It also self-contained. It has many descendants: RHEL, FreeBSD, OpenBSD. They are not "Unix" systems but "Unix-like". To use word Unix you should pay a fees, etc to Open Group. 

* `unix-like system` - definition

Finally, Linux appeared to put all dots on i as separate project. It's a kernel *only*. Self-contained systems are *distributions* in this context which are Ubuntu, Debian, etc..

POSIX appeared?
* `POSIX` - defines set of fundamental abstractions and organization needed for efficient construction of apps which can interoperate between different "flavours" of Unix/Unix-like systems. See https://stackoverflow.com/questions/1780599/i-never-really-understood-what-is-posix#31865755.
* `POSIX-compliant` - program or operating system that follows that standard.

![unix history tree](https://qph.fs.quoracdn.net/main-qimg-b2f5ed77ec03ade04f922cb32ea0ce6a)

### Unix-like system consists of
* kernel
* shell
* fs
* dev environment
* commands
* documentation

### Man pages
* `Man pages` - manual pages about the program
    * `nroff -man mymanpage.1 | less` to read

## A bit on Windows-world
There is a history behind porting what people get used to in Unix to Windows world. 

* MSYS + MinGW vs Cygwin
* MSYS2 is everything above + `pacman` package manager
