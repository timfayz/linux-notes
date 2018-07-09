# linux-notes

## Coding pages
[Table Of Content](url)
* Get hands dirty
    * Prepare Linux (VM, LiveCD)
    * First Boot
    * Play Around
    * Write & Run "Hello world"
* Theory
    * PC Boot Process
    * Linux Boot Process
    * Linux organization & management
    * Scripting
    ...
    * Built by yourself (link)
* Compose own Linux
    * Void, Xorg, dwm, st, etc

## First approximation (basic)
```
/boot
/dev
/etc
/sys
/proc
/usr
```

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

## Useful tools
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

## Important Linux conventions
```
$ - ordinary user
# - root

./ - current dir
../ - parent dir

named - 'd' is certainly daemon (background process/service)
```
