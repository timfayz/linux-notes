# Unix Toolbox

## Compile & Run programs
```bash
# NASM
# -f: output file format (-hf to list)
# -F: debug information output (-felf -y to list)
# -g: generate debugging information
# -l file: generate listing to file
# -o file: precise name for the output (default as source)
# -a: do not preprocess file (if used as back-end)
# -E: preprocess only
nasm -f elf file.asm -l file.lst

# LINKER
# -o fine: name for resulting executable
# -e/--entry=entry: use entry as explicit symbol for beginning execution of the program, rather than the default. Entry can be a number to specify address (16 or 0x10)
# -EB/-EL: link big/little-endian objects
# -m: emulate the emulation linker
# -M/--print-map: print a link map to stdout
# -O level: optimize output. Only affects ELF shared library generation
# -r/--relocatable: generate relocatable output, i.e. file that can in turn server as input to ld. Often called "partial linking". Option does the same as -i
# -s/--strip-all: omit all symbol information from output
# -S/--strip-debug: omit debugger symbol information
# -V/--verbose: to lists supported emulations
# -T/--script=file: use file as the linker script. See info ld
# difference b/w emulation modes: https://stackoverflow.com/a/39028477/1349754
# emulation mode mainly output format, arch, PT load address
# related option: -z max-page-size=0x1000
ld -m elf_i386 file.o -o file -T script.lds

# GCC/AS/CC
# generate assembly listing interlaced with source
# -v: to see precisely what options it passes to each compilation pass, including the assembler, linker, etc.
# -c: compile or assemble the source file, but do not link (gen objects for each source)
# -S: stop before assembling (gen assembly for each source)
# -m64: generate code for 32/64-bit environment
# -o: output name to whatever sort of output is being produced
#
# -Wa,option: pass options to the assembler
#    a: generate listing 
#    l: include assembly
#    h: include high-level source
# -Wl,option: pass options to linker
# -Wl,--start-group ... Wl,--end-group
# -Wl,-oVALUE1 -Wl,-oVALUE2
#
# -masm=dialect: output assembly instructions using selected dialect (att or intel)
# -g: produce debugging information in the operating system's native format (stabs, COFF, XCOFF, or DWARF)
# -fno-asynchronous-unwind-tables: do not generate unwind table in DWARF format
# -fno-dwarf2-cfi-asm: Emit DWARF unwind info as compiler generated ".eh_frame" section instead of using GAS ".cfi_*" directives
# todo
# -fPIC: Position Independent Code
# -no-pie: 
# -shared: create a shared object file
# -nostdlib & -nostartfiles: 
gcc -fno-dwarf2-cfi-asm -fno-asynchronous-unwind-tables -Wa,-adhln file.c > file.lst # disassebly

# OBJDUMP
# -p/--private-headers
# -x/--all-headers 
# -d/--disassemble
# -M/--disassembler-options=options, eg -Mintel
objdump -x file
objdump --no-show-raw-insn -d -Mintel a.out 

# READELF
# -a/--all: display all headers
# -h/--file-header: display ELF file header
readelf -a file

# TODO
nm
hexview
ndisasm -b 64 filename
strace
gdb
execve()
exec
chpst
"stabs info"?
```

## Documentation and help
```bash
whatis [program] // list pages
man [-number] [program]
```

### General system management
```bash
pstree
top/htop
dmesg
log
```

### Device management
```bash
udev
lsblk
blkid
```

### File management
```bash
ls
mkdir
cp/scp/rsync
chown
chmod
```

### Search and location
```bash
which X
locate
find
```

### File system management
```bash
mount
mkfs.*
```

### User management
```bash
id
groups
passwd
useradd
usermod
```

### Remote access
```bash
ssh
```
