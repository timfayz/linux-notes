# linux-notes
This is how I become aweare of what's going on in Linux

### Table Of Content
* [Prepare Linux](https://github.com/timfayz/simply-linux) <br>
Get hands dirty. Bootstraping yourself. Before extending the system become good user of it.
    * Search and location
    * Documentation and help
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
