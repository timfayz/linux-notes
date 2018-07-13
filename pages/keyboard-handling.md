## Keyboard handling
Roughly speaking, the picture is this: the keyboard produces scancodes, the scancodes are assembled into keycodes (one unique code for each key), and keycodes are converted to tty input characters using the kernel keymaps. After that, the normal `stty` processing takes place, just as for any other terminal.

In a Linux console, keycodes are mapped to escape sequences according to the console keymap.

The mapping uses two levels of indirection, from keycode+modifier combination (with three modifiers: shift, control, alt) to keysym and from keysym to string (character or escape sequence). The set of keysyms is fixed, so if you want to define custom combinations you'll need to use existing keysyms that aren't otherwise used such as F13, F14, …
 
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

