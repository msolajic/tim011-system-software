# tim011-system-software
System software for TIM011, a school computer from the end of 1980's made in former Yugoslavia

BIOS is based on BIOS 3.2 for Micromint SB180.
Boot ROM is based on Monitor 1.0 for MicroMint SB180.

### CompactFlash version
This version of the BIOS removes the support for SCSI hard disks, and adds support for CompactFlash cards in 8-bit mode, LBA addressed.
A 32MB or larger CompactFlash card is needed. BIOS has been set up so a 32MB card can be used fully (3 8-megabyte partitions and one 6.7Mb in size). First partition is lightly smaller so a system image can be loaded onto it.
Routines are adapted from Grant Searle' Z80 SBC.
Hardware interface schematic is attached, and full interface PCB will be available soon.

### Compiling and making a working boot floppy
Compile with the tools in the root directory:
CPM ZAS CFBIOS
CPM ZLINK CFBIOS $RCF00
You need to inject the compiled BIOS, CFBIOS.COM into a working floppy image. Using a hex editor of choice, overlay the first 1000h bytes into floppy disk image at offset 1680h.
If modifying, care must be taken because some routines and buffers cannot move from their original place in memory (to avoid recompiling more supporting files)

### Usage
For now, no tools for initializing the card are available. Please dump the provided hard disk image file to a CompactFlash card.
Boot the computer from tim011_boot_cf_system.img floppy image. At boot, CompactFlash card will be detected and initialized. If it is available, drives E-H will be assigned to it. You can use the CDC command to switch the card to be A-D and floppies E-H.
When you have a verified working system, you can use tim011_boot_direct_from_cf.img which will load everything (except the system image) off the card, and the drive letters A-D will be assigned to the card automatically.
An updated Boot ROM will be made available soon with the ability to detect the card and if it contains the system image, and boot directly from it.

---

I am not sure about the licensing. TIM011 is both software and hardware wise strongly based on SB180 single board computer from Micromint, amd uses ZRDOS and ZCPR3 by Echelon. No documentation has been ever made available from the manufacturer, Institute "Mihajlo Pupin" from Belgrade regarding system software. As a long time has passed since, I think nobody will object for the code to be available.
