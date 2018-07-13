# linux-notes
This is how I become aweare of what's going on in Linux

### Table Of Content
* [Prepare Linux](https://github.com/timfayz/simply-linux) <br>
Bootstraping yourself. Get hands dirty. Before extending the system - become part of or get used to it. 
* [PC Boot Process](pages/pc-boot.md)  
* Write & Run "Hello world"
* What every programmer should know about symbols displayed on screen
* Linux organization & management
* Scripting
...
* [Built your own Linux](http://www.linuxfromscratch.org/blfs/)



## Unsroted
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

**Useful tools**
```
### General system management
pstree
top/htop
dmesg
log

### Device management
udev
lsblk
blkid

### File management
ls
find
cp/scp/rsync
chown
chmod

### File system management
mount
mkfs.*

### User management
id
groups
passwd
useradd
usermod

### Run programs
exec
chpst

### Search and location
which X

### Documentation and help
whatis X

### Password management
### Remote access
ssh
```

