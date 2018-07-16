## Keyboard handling
Roughly speaking, the picture is this: the keyboard produces scancodes, the scancodes are assembled into keycodes (one unique code for each key), and keycodes are converted to tty input characters using the kernel keymaps. After that, the normal `stty` processing takes place, just as for any other terminal.

The mapping uses two levels of indirection, from keycode+modifier combination (with three modifiers: shift, control, alt) to keysym and from keysym to string (character or escape sequence). The set of keysyms is fixed, so if you want to define custom combinations you'll need to use existing keysyms that aren't otherwise used such as F13, F14, …

### X Server
The X server reads input events through a device file, for example `/dev/input/eventNN`

SPLIT X11 PLAIN LINUX CONSOLE (DO NOT MESS!)
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
+-------------+        +----------+          +-----+         +---------+
| application |------->| X server |---····-->| GPU |-------->| monitor |
+-------------+        +----------+          +-----+         +---------+
               text or              varies          VGA, DVI,
               image                                HDMI, …
```
There are two ways to display a character.

* Server-side rendering: the application tells the X server “draw this string in this font at this position”. The font resides on the X server.
* Client-side rendering: the application builds an image that represents the character in a font that it chooses, then tells the X server to display that image.

#### Programs
* `xset q` - show current X11 properties
* `mkfontdir` - generate font index storing aliases into `font.alias` (bitmap) and `font.scale` (vector)

#### Files
* `/usr/share/fonts/*/fonts.{alias,scale}`

### Console
In a Linux console, keycodes are mapped to escape sequences according to the console keymap.

As for the Linux console, it has its own keyboard layouts which are stored in /usr/share/keymaps and loaded with the loadkeys command. When in the BIOS and earlier boot loader stages, including GRUB2, the keyboard mapping is whatever the number the BIOS decides to map the key to.


#### References
[1] https://unix.stackexchange.com/questions/116629/how-do-keyboard-input-and-text-output-work/116630#116630
[2] https://unix.stackexchange.com/questions/12510/relationship-of-keyboard-layout-and-xmodmap/12518#12518
[1] (MOVE TO FONT SECTION) https://unix.stackexchange.com/questions/111454/what-are-the-purposes-of-the-different-types-of-xwindows-fonts/111576#111576

#### Tools (runtime management)
* `setkeycodes`
* `loadkeys`
* `showconsolefont`
* `showkey`

#### Files (persistent configuration)
* `/dev/input/event*`
