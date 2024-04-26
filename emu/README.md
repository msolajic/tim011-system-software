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

## TIM 011 keyboard

The keyboard sends characters by serial port, at 9600 N8E. It has a CDP1802 CPU, ROM and a lot of TTL logic inside. It can also receive codes, for controlling the LEDs, typematic rate, and playing simple sounds.

Almost all keys which are not characters (punctuation, brackets, arrows etc) send non-standard codes. Terminal emulator translates these codes in two ways, either by simple subtraction, or by means of a translation table. This translation table can be changed, to support national keycodes (latin and cyrillic ŠĐČĆŽ). Also, the function keys have their own definition table, which can be changed by, for example, BASIC interpreter. Here is the breakdown of all keys, their corresponding codes, if they have a translation entry, and to which code the keypress translates to.

|Key         |code sent|table entry|translated to           |
|------------|---------|-----------|------------------------|
|SET UP      |0x80     |           |0x00                    |
|}           |0xad     |0x2d       |0x7d                    |
|`           |0xb0     |0x30       |0x60                    |
|{           |0xbb     |0x3b       |0x7b                    |
|\|          |0xbc     |0x3c       |0x7c                    |
|]           |0xbd     |0x3d       |0x5d                    |
|~           |0xbe     |0x3e       |0x7e                    |
|@           |0xc0     |0x40       |0x40                    |
|up arrow    |0xc1     |0x41       |0x05 (CTL-E)            |
|down arrow  |0xc2     |0x42       |0x18 (CTL-X)            |
|right arrow |0xc3     |0x43       |0x04 (CTL-D)            |
|left arrow  |0xc4     |0x44       |0x13 (CTL-S)            |
|[           |0xcb     |0x4b       |0x5b                    |
|\           |0xcc     |0x4c       |0x5c                    |
|numpad enter|0xcd     |           |0x0d                    |
|^           |0xce     |0x4e       |0x5e                    |
|PF1         |0xd0     |0x50       |0x12 (CTL-R)            |
|PF2         |0xd1     |0x51       |0x03 (CTL-C)            |
|PF3         |0xd2     |0x52       |0x01 (CTL-A             |
|PF4         |0xd3     |0x53       |0x06 (CTL-F             |
|F1          |0xd4     |           |                        |
|F2          |0xd5     |           |                        |
|F3          |0xd6     |           |                        |
|F4          |0xd7     |           |                        |
|F5          |0xd8     |           |                        |
|F6          |0xd9     |           |                        |
|F7          |0xda     |           |                        |
|F8          |0xdb     |           |                        |
|F9          |0xdc     |           |                        |
|F10         |0xdd     |           |                        |
|F11         |0xde     |           |                        |
|CTL-COPY    |0xdf     |           |                        |
|numpad ,    |0xec     |           |0x2c                    |
|numpad -    |0xed     |           |0x2d                    |
|numpad .    |0xee     |           |0x2e                    |
|numpad 0    |0xf0     |           |0x30                    |
|numpad 1    |0xf1     |           |0x31                    |
|numpad 2    |0xf2     |           |0x32                    |
|numpad 3    |0xf3     |           |0x33                    |
|numpad 4    |0xf4     |           |0x34                    |
|numpad 5    |0xf5     |           |0x35                    |
|numpad 6    |0xf6     |           |0x36                    |
|numpad 7    |0xf7     |           |0x37                    |
|numpad 8    |0xf8     |           |0x38                    |
|numpad 9    |0xf9     |           |0x39                    |
|BRK         |0xfa     |0x7a       |0x03 (CTL-C)            |
|CTL-BRK     |0xfb     |0x7b       |0x03 (CTL-C)            |