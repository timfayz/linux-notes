# PC boot
This document describes how typical Linux system boots on PC. It mostly concerns by which order programs start (process tree) and what the files are either created, read or removed during this boot. It is an attempt to make an overall picture how Linux started on process+data level with no cognitive pain :) I assume the only two things - you occasionally stumbled upon running Linux system with either GUI/Desktop environment or just CLI; and you know basics of comand line interface.

## Second approximation (advanced)
### Linux boot process on BIOS system
1. System switched on and power-on-self-test (POST)
1. BIOS firmware is loaded and it initializes hardware (scan available mediums)
1. Firmware loads first 440 bytes of the first medium in the BIOS disk order
1. MBR code takes control and loads/jump to next stage Bootloader code
1. Bootloader takes control, read configs and load kernel & initramfs (initrd) into RAM
1. Kernel takes control, load necessary modules, unpack/mount initramfs as temp root
1. \* When the kernel detects a new device, it runs the program modprobe and passes it a name that identifies the device. Most devices are identified through registered numbers for a vendor and model, e.g. PCI or USB identifiers. The modprobe program consults the module alias table /lib/modules/VERSION/modules.alias to find the name of the file that contains the driver for that particular device.
1. initramfs runs `init` script, create /newroot, create dev nodes, mount file systems (/dev, /sys, etc), configs, load modules (eg those kernel don’t have or need for first boot), unload them from RAM and chrooting to /
1. Service manager (OpenRC, runit, systemd, etc) takes control

### Boot process under UEFI
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
