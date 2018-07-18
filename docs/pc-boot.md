# Device boot
This document describes how typical Linux system boots under PC/ARM. It mostly concerns by which order programs start (process tree) and what the files are either created, read or removed during this boot.

## PC (x86, x86_64, i386, amd64)
This is how boot process is done under BIOS/UEFI firmwares. The are list of the most important things you need aware of.

### BIOS
1. **Power on**
1. **ROM firmware is loaded** 
    * Power-on-self-test ([POST](https://en.wikipedia.org/wiki/Power-on_self-test))
    * Hardware initialization and scaning for available mediums
1. **[Stage 1]** Firmware loads **first 440 bytes** of the first medium according to "boot order"
    * GRUB(2): `/usr/lib/grub/i386-pc/boot.image, cdboot.image, etc`
    * Syslinux: `/usr/share/syslinux/mbr.bin, gptmbr.bin, etc`
1. **[Stage 1]** Search active partition. The Stage 1 MBR boot code looks for the partition that is marked as active (*boot flag* under MBR, or *legacy BIOS bootable* under GPT). Let us assume this is the `/boot` partition, for example.

1. Master Boot Code (w/e GPT or MBR) takes control and loads/jump to next stage Bootloader code
1. Bootloader (SYSLINUX, GRUB, etc) takes control, read configs and load kernel & initramfs (initrd) into RAM
1. Kernel takes control, load necessary modules, unpack/mount initramfs as temp root
1. \* When the kernel detects a new device, it runs the program modprobe and passes it a name that identifies the device. Most devices are identified through registered numbers for a vendor and model, e.g. PCI or USB identifiers. The modprobe program consults the module alias table /lib/modules/VERSION/modules.alias to find the name of the file that contains the driver for that particular device.
1. initramfs runs `init` script, create /newroot, create dev nodes, mount file systems (/dev, /sys, etc), configs, load modules (eg those kernel don’t have or need for first boot), unload them from RAM and chrooting to /
1. Service manager (OpenRC, runit, systemd, etc) takes control

### UEFI
1. UEFI firmware is loaded and it initializes hardware required for booting
1. Firmware reads boot entries in the firmware's boot manager to determine which UEFI application to be launched and from where (i.e. which disk and partition).
1. Firmware launches the UEFI application* which could be:
    * Linux itself (if EFISTUB is enabled)
    * Other application such as a shell or a graphical boot manager.
    * Simply a disk. In this case the firmware looks for ESP on that disk and tries to run fallback UEFI application \EFI\BOOT\BOOTX64.EFI (this is how UEFI bootable thumb drives work)
1. The same as BIOS (step 6+)

\* *If Secure Boot is enabled, boot process verifies authenticity of EFI binary by signature at first.*

4. a
4. b
### BIOS/UEFI important notes
* BIOS and UEFI are different types of ROM firmware
* BIOS has no idea what is “partition”
* BIOS inits hardware, load MBR code from particular disk and run it
* UEFI support disks, partitions (GPT), filesystems and can load EFI executable in specified format from (FAT-based) EFI system partition (similar to MBR code)

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
