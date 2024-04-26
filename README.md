# tim011-system-software
System software for TIM011, a school computer from the end of 1980's made in former Yugoslavia

BIOS is based on BIOS 3.2 for Micromint SB180.
Boot ROM is based on Monitor 1.0 for MicroMint SB180.

### Update 26. April 2024.
Added the assembly listing of main payload of EMU terminal emulator, accompanying loader, and character set.

Some cross-references in BIOS properly commented.

This needs more work, mainly in how to assemble it, but assembling the main payload creates a binary equivalent of the original payload.

### Update 17. April 2024.
Added reconstructed assembly for Boot ROM, pckbd.iop and pckbd.com (PC Keyboard support routines).

Fixed BIOS error where ASCI0 has interrupts enabled, but no ISR defined, so any received data trough serial port will cause a "Interrupt error" and lock up the computer.

Commented thoroughly for (mostly) all the changes made to the original.

---

Original BIOS assembly files for SB180 are uploaded for reference, so you can make a diff between the modified BIOS and the originals.

I am not sure about the licensing. TIM011 is both software and hardware wise strongly based on SB180 single board computer from Micromint, amd uses ZRDOS and ZCPR3 by Echelon. No documentation has been ever made available from the manufacturer, Institute "Mihajlo Pupin" from Belgrade regarding system software. As a long time has passed since, I think nobody will object for the code to be available.
