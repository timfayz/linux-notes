# linux-notes

## Basic conception
* `access` - in order to change something you an access.
* `configuration` - you want your setup to persist in time on each boot.
* `session` - you want several typical layouts to work with something.


## Keyboard handling
Roughly speaking, the picture is this: the keyboard produces scancodes, the scancodes are assembled into keycodes (one unique code for each key), and keycodes are converted to tty input characters using the kernel keymaps. After that, the normal `stty` processing takes place, just as for any other terminal.

In a Linux console, keycodes are mapped to escape sequences according to the console keymap.

The mapping uses two levels of indirection, from keycode+modifier combination (with three modifiers: shift, control, alt) to keysym and from keysym to string (character or escape sequence). The set of keysyms is fixed, so if you want to define custom combinations you'll need to use existing keysyms that aren't otherwise used such as F13, F14, …
 
```
Keyboard (3 types of scancodes) --[scancode]--> Motherboard --> 
CPU --[interrup]--> Linux kernel (ioctl) --[keycode]-->
  Console driver --[escape sequence]--> Shell  
  X Server --[keysyms+modifiers]--> Application
```
```
[INPUT]
+----------+              +-------------+         +-----+
| keyboard |------------->| motherboard |-------->| CPU |
+----------+              +-------------+         +-----+
(3 types of scancodes)
             USB, PS/2, …                 PCI, …
             key down/up

         +--------+        +----------+          +-------------+
-------->| kernel |------->| X server |--------->| application |
         +--------+        +----------+          +-------------+
interrupt          scancode             keysym
                   =keycode            +modifiers
OR
         +--------+         +----------------+          +-------+
-------->| kernel |-------->| console driver |--------->| shell |
         +--------+         +----------------+          +-------+
interrupt (ioctl)   keycode                   escape 
                                              sequence

[OUTPUT]
```
#### Reference
[1] https://unix.stackexchange.com/questions/116629/how-do-keyboard-input-and-text-output-work/116630#116630



#### PROGS (to manage runtime)
* `setkeycodes`
* `loadkeys`
* `showconsolefont`
* `showkey`

#### FILES (to configure)
* `/dev/input/event*`


## Characters and Encoding
* `Character` - is the smallest *element of meaning*. It can be letter, spacing character, symbol or even a word. 
Examples: A B | + $ etc.

* `Character Set` (or `charset`) - is a *collection* of that characters (sometimes mistakenly synonymous with *Code Page*; they are related but not the same). Each Character in the collection has a *Code Point* or a unique number. One charset might be used by multiple languages. For example, latin letters are used in various European languages. In general, most of charsets are formed naturally and united under some category. As a rule, charsets are collections without a method of *Encoding* them (or representing in machine readable form).
Examples: Unicode (UCS), language alphabets, greek numbers, etc.

* `Encoding` -  it is *how* a mapping between Character Set and machine readable form of its Characters is done. Often used interchangeably with the Code Page term (which is good way to go). However, Encoding has more general sense and might include the latter. Examples fit to both Encodings and Code Pages: UTF-8/16, ASCII, KOI8, ISO 8859 (Latin-1), Windows-1252 (CP-1252), CP437, etc. 

* `Code Page` (or `coded character sets`) - is a *table* where each Character has been assigned a *unique* number. Code Pages could contain multiple charsets imposed on the same table with one method of Encoding. Think of Code Pages being a conventional table of Characters mapped to (human readable) numbers and Encodings being a program technique of how that Characters must be encoded to (machine readable) byte form. 

* `Code Point` - is a *unique number* assigned to a Character that makes up a *Code Space* of Character Set.

* `Glyph` - is a *graphical representation* of a Character. Character can be one but has several glyphs. Examples: Α, *Α*, **Α**.

```
[            256-65536] - ISO 10646, UCS, Universal Character Set or just Unicode (16/32bit)
[     128-255]          - ISO 8859-1, CP-1252, KOI8 (8bit)
[0-127]                 - US-ASCII or just "classic" ASCII (7bit)
First 0-65536(0xFFFF) code points of Unicode are "basic multilingual plane" (BMP), all other are "supplementary characters"
```

References:
1. https://blogs.msdn.microsoft.com/shawnste/2005/03/15/whats-the-difference-between-an-encoding-code-page-character-set-and-unicode/
1. https://en.wikipedia.org/wiki/Character_encoding#Terminology
1. https://stackoverflow.com/questions/3441490/whats-the-difference-between-an-encoding-a-character-set-and-a-code-page

#### PROGS
* `iconv`

#### FILES

## Fonts and rendering

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
    * What every programmer should know about symbols displayed on screen
    * Linux organization & management
    * Scripting
    ...
    * Built by yourself (link)
* Compose own Linux
    * Void, Xorg, dwm, st, etc
