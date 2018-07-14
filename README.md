# linux-notes
This is how I become aweare of what's going on in Linux

### Table Of Content
* [Prepare Linux](https://github.com/timfayz/simply-linux) <br>
Bootstraping yourself. Get hands dirty. Before extending the system - become part of or get used to it. 
* [PC Boot Process](pages/pc-boot.md) <br>
Understand how your PC booting up whatever regardless of the OS.
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



## Unsroted
* [Toolbox](pages/toolbox.md)
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
chpst

### Search and location
which X

### Documentation and help
whatis X

### Password management
### Remote access
ssh
```
