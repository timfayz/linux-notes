# Boot process
This document describes how typical Linux system boots under PC/ARM. It mostly concerns by which order programs start (process tree) and what the files are either created, read or removed during this boot. It is an attempt to make an overall picture how Linux started on process+data level with no cognitive pain :]

## Overview
```
(power on)

0. |CPU| -> loads motherboard ROM firmware 

1. |BIOS/UEFI| -> inits hardware, check itegrity, scan for available
   mediums and load medium's MBR code according to "boot order"

2. |MBR code| -> jumps to `bootloader`

3. |bootloader| -> search and loads configurations

4. |kernel| -> 

5. |initramfs| -> 

6. |init| -> 
   (user space configuration)

(login promt)
```

## PC
*aliases: x86, x86_64, i386, amd64* 1<br>

### BIOS
1. System switch on and power-on-self-test (POST)
1. BIOS firmware is loaded and it initializes hardware (scan available mediums)
1. Firmware loads first 440 bytes of the first medium in the BIOS disk order
1. Master Boot Code (regardless GPT or MBR) takes control (Stage 1), search for active partition marked as "active" (*boot flag* under MBR, or *legacy BIOS bootable* under GPT), then loads/jumps to the next stage Bootloader code
1. Bootloader (SYSLINUX, GRUB, etc) takes control (Stage 2), read configs and load kernel and initramfs (initrd) into RAM
1. Kernel takes control (vmlinuz), load necessary modules, unpack/mount initramfs as temp root
1. \* When the kernel detects a new device, it runs the program modprobe and passes it a name that identifies the device. Most devices are identified through registered numbers for a vendor and model, e.g. PCI or USB identifiers. The modprobe program consults the module alias table `/lib/modules/VERSION/modules.alias` to find the name of the file that contains the driver for that particular device.
1. initramfs runs `init` script, create /newroot, create dev nodes, mount file systems (`/dev`, `/sys`, etc), configs, load modules (eg those kernel don’t have or need for first boot), unload them from RAM and chrooting to `/`
1. Service manager (OpenRC, runit, systemd, etc) takes control and runs services in background

### UEFI
1. UEFI firmware is loaded and it initializes hardware required for booting
1. Firmware reads boot entries in the firmware's boot manager to determine which UEFI application to be launched and from where (i.e. which disk and partition).
1. Firmware launches the UEFI application* which could be:
    * Linux itself (if EFISTUB is enabled)
    * Other application such as a shell or a graphical boot manager.
    * Simply a disk. In this case the firmware looks for ESP on that disk and tries to run fallback UEFI application \EFI\BOOT\BOOTX64.EFI (this is how UEFI bootable thumb drives work)
1. The same as BIOS (step 6+)

\* *If Secure Boot is enabled, boot process verifies authenticity of EFI binary by signature at first.*

### BIOS/UEFI important notes
* BIOS and UEFI are different types of ROM firmware
* BIOS has no idea what is “partition”
* BIOS inits hardware, load MBR code from particular disk and run it
* UEFI support disks, partitions (GPT), filesystems and can load EFI executable in specified format from (FAT-based) EFI system partition (similar to MBR code)

## ARM
*aliases: aarch64, armv6/7/8, rpi/2/3, beagleboard, odroid, etc.*

https://raspberrypi.stackexchange.com/questions/8475/what-bios-does-raspberry-pi-use

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
