# linux-notes

## Coding pages

### Main definitions
* `Character` - the smallest *element of meaning*. It can be letter, spacing character, symbol or even a word. Examples: A B | + $ etc.
* `Character Set` (or `charset`) - just a *collection* of that characters (sometimes referenced with *Code Page*). That a set might be used by multiple languages like latin letters used in different European languages. Like any Character, the sets are mostly formed naturally. Character Sets are generally collections without a method of *Encoding* them (like an alphabet without assigned some unique numbers to them). On the contrary, code pages could contain multiple sets of characters. Examples: natural language alphabets, Unicode, greek/arabic numbers, etc.
* `Code Page` (or `coded character sets`) - a *table* where each character (of any of its character set) has been assigned a number. Think of Code Pages being similar to a table of characters to number and Encodings being how the characters get from Character to encoded byte form. Examples: Unicode (UCS), ASCII, KOI8, ISO 8859 (Latin-1), Windows-1252 (CP-1252), etc.
* `Encoding` -  a *mapping* between a Character Set and a (usually byte-based) technical representation of the characters.
* `Code Point` - a *unique number* assigned to a character that makes up a *code space* of Character Set.
* `Glyph` - *graphical representation* of a Character. Character can be one but to has several glyphs. Examples: Α, *Α*, **Α**.

### Byte representation
```
[            256-65536] - ISO 10646, UCS, Universal Character Set or just Unicode (16/32bit)
[     128-255]          - ISO 8859-1, CP-1252, KOI8 (8bit)
[0-127]                 - US-ASCII or just "classic" ASCII (7bit)
First 0-65536(0xFFFF) code points of Unicode are "basic multilingual plane" (BMP), all other are "supplementary characters"
```

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

programd - `d` stands for daemon (background process/service)
/path/to/program.conf.d/ - `.conf.d` is pool of configuration files which is typicaly loaded during the program start
```


## TODO
Future [Table Of Content](url)
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
