# Troll static test-drive files

This directory contains the files needed to operate the *troll*
debugger in a so-called *static test-drive* mode.
This is similar to working with *core* files from within the *gdb* debugger.
In this mode, no connection to a live target system is established, and
instead the *troll* reads the contents of target memory and registers
from files. In this mode, the *troll* does not invoke any external
tools it otherwise relies upon, and all necessary data for the *troll*'s
operation is being fetched from files with hard-coded names.
This *static test-drive mode of operation* is intended for *troll*
rapid prototyping and debugging and demonstration of the capabilities
of the *troll*.

These are the files needed by the *troll* when operating in
a *static test-drive mode* - all of the files must reside in a
directory named `troll-test-drive-files`, which must reside in
the *troll*'s working directory:

- `blackmagic.elf`
- `blackmagic.elf.srec`
- `disassembly.txt`
- `elf-sections-dump.txt`
- `flash.bin`
- `ram.bin`
- `registers.bin`

Additionally, the source code of the target program that is being debugged,
must reside in a subdirectory named `blackmagic` in the `troll-test-drive-files`
directory.

Here are more details which file is what:

- `blackmagic.elf` - the *ELF* formatted compiled executable file of the program that is being debugged
- `blackmagic.elf.srec` - an *s-record* formatted file which contains the target memory area
contents from the compiled executable file, which reside in target non-volatile memory
(e.g. *flash* memory).
This file is created by executing the command:
`arm-none-eabi-objcopy -O srec blackmagic.elf blackmagic.elf.srec`
- `disassembly.txt` - disassembly dump of the program that is being debugged.
This file is created by executing the command:
`arm-none-eabi-objdump -d -S blackmagic.elf > disassembly.txt`
- `elf-sections-dump.txt` - a dump of the *ELF* section headers of the *ELF* formatted file that
is being debugged.
This file is created by executing the command:
`arm-none-eabi-objdump -h blackmagic.elf > elf-sections-dump.txt`
- `flash.bin` - binary dump of the target *flash* memory contents at the time the target was
previously halted in order to examine its state. This file must be exactly 128 kB in size.
- `ram.bin` - binary dump of the target *ram* memory contents at the time the target was
previously halted in order to examine its state. This file must be exactly 128 kB in size.
- `registers.bin` - binary dump of the target *general purpose registers *contents at the time
the target was previously halted in order to examine its state.
This file must be exactly 64 bytes in size.

