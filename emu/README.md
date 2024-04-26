This disassembly has been possible by the use of MAME emulator with it's debugger and Ghidra.
This program forms the part of the TIM 011 BIOS, where functions of drawing the characters to screen memory,
processing keyboard input, cursor movement and blinking etc have been moved from the BIOS.
My comments leave much to desire, as this code is very convoluted.

While decompiling, some unknown code from the BIOS has been "decyphered" and also further cross-dependencies found.
One routine from BIOS copies the F_KEYS_TABLE_BACKUP to F_KEYS_TABLE_MAIN on every warm start.
This is so other programs can write their own table to F_KEYS_TABLE_MAIN and redefine the function keys.
Only example found so far is the BASIC interpreter included on the system disk, which redefines all function keys.

Also, the program depends on the location of type-ahead buffer in the BIOS, and you have to define this address.

Characters are in a 6x10 matrix, externally redefinable by use of CIR.COM, LAT.COM or ASC.COM
These programs will try to find the location of character definitions by reading the address from CHARSET_LOCATION, 
but will blindly overwrite anything to the hardcoded location of TRANSLATION_TABLE so they can support national alphabets.

So, in my opinion, modifications of this program are not recommended. You have been advised.

Compiled code of EMU.Z80 has to be included in EMU_LOADER.Z80 output. I don't know how yet.
probably on a real machine, make both as com files, and load load the loader to 0100h and this to 0200h, then save as one com file.
I will update this as soon as possible.