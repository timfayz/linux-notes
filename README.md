# Linux Notes
This is how I become aweare of what's going on in the Linux. This is kinda of framework to ask questions about the Linux *properly*.

### Table Of Content
* [Bootstrapping](https://github.com/timfayz/simply-linux) <br>
Get hands dirty. Bootstraping yourself. Before extending the system become good user of it.
    * Search and location
    * Documentation and help
* [PC Boot Process](pages/pc-boot.md) <br>
Understand how your PC booting up regardless of the OS you use.
* Linux Internals <br>
Organization & management
    * [Basic concepts](pages/basic-concepts.md)
    * [Characters and encodings](pages/charset-encoding.md)
    * [Font rendering](pages/font-rendering.md)
    * [Keyboard handling](pages/keyboard-handling.md)
* Write & Run "Hello world"
* Scripting
...
* [Built your own Linux](http://www.linuxfromscratch.org/blfs/)

### Little TODO
* move pages/ to docs/

### Definition of being able to manage
**manage** Linux program means _know how to_:
* show its location
* show its permissions, user, group
* change its state during 
    * **first boot** (using configuration)
    * **runtime** (using command line or reloading configs)
* build it from sources
* list its dependecies (ldd)
* list network ports it uses
* list systemcalls it calls
* measure performance (profiling) 
* show the platform it was compiled against
* use it (flags & options) under CLI
* show how much memory and CPU it utilize
* find it man page, docs, reference, etc

Main questions:
1. Which programs manage smthg?
1. Where they are stored?
1. Where their configs are stored?
1. How to change them?
1. How to check the changes?
1. (if defaults hardcoded) Can I recompile program to change its defaults?
1. (if nothing found) What the syscalls/libraries it uses?
1. Can I write my own program to do what I want?

## Unsroted
* [Toolbox](pages/toolbox.md)
* [Template](pages/template.md)
* [Linux conventions](pages/linux-conventions.md)
* What every programmer should know about symbols displayed on screen
```
(kernel space)
[syslinux/grub] -> [vmlinuz] -> [initramfs] -> [runit] ->

(user space)
[login (/car/utmp,/etc/passwd)] -> [tmux [slstatus]]
-> [Xorg] -> [dwm] -> [st]
or
[agetty*] -> [login] -> [sh]

sudo chsh -s /usr/bin/tmux $USER
```
