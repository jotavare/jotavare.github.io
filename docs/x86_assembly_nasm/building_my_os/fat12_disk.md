---
title: FAT12 Disk
nav_order: 4
layout: default
parent: Building My OS
grand_parent: 🔲 x86 Assembly NASM
---

## **FAT12 Disk**

In this example, I will build on top of the previous code and build an **OS** (operating system), starting from the boot process and diving into the creation of a file system. I'll cover the structure of a traditional OS, the role of a bootloader and kernel, formatting a disk using **FAT12 file system**, and integrating **bootloader** and **kernel** into a disk image.

### **OS Structure**

In most traditional operating systems, there are two main components:

- **Bootloader**
  - The bootloader plays a crucial role in setting up the system;
  - It gathers system information and prepares the environment for the kernel;
  - Additionally, it loads the kernel into memory, enabling it to execute OS operations;

- ***Kernel***
  - The kernel is responsible for performing all core OS functions;
  - It manages system resources, handles system calls, and orchestrates various system operations;

- **Preparation**
  - Organize project files into separate folders for **bootloader** and **kernel**;
  - Modify the `Makefile` to accommodate separate rules for compiling **bootloader** and **kernel**;

**Project Structure:**

In this project, I'm gonna work with the files with `*`:

```
fat12_disk
├── Makefile* 
├── bootloader
│   └── boot.asm*
└── kernel
    └── main.asm (optional at the moment)
```

{: .important-title }
A significant challenge in OS development is working within the constraints of the boot disk. Typically, a boot disk, such as a floppy disk, provides limited storage space, typically around `512 bytes` per sector. This limitation necessitates efficient utilization of disk space, especially when accommodating both the bootloader and kernel.

----

### **Makefile Configuration**

This `Makefile` organizes the compilation of the bootloader and kernel, as well as the creation of the boot disk image (`main.img`).

```makefile
# Assembler
ASM=nasm

# Directories
SRC_DIR=src
BUILD_DIR=build

# Floopy disk
floopy_image: $(BUILD_DIR)/main.img
$(BUILD_DIR)/main.img: bootloader kernel
	dd if=/dev/zero of=$(BUILD_DIR)/main.img bs=512 count=2880
	mkfs.fat -F 12 -n "FAT12" $(BUILD_DIR)/main.img
	dd if=$(BUILD_DIR)/bootloader.bin of=$(BUILD_DIR)/main.img conv=notrunc
	mcopy -i $(BUILD_DIR)/main.img $(BUILD_DIR)/kernel.bin "::kernel.bin"

# Bootloader
bootloader: $(BUILD_DIR)/bootloader.bin
$(BUILD_DIR)/bootloader.bin:
	$(ASM) $(SRC_DIR)/bootloader/boot.asm -f bin -o $(BUILD_DIR)/bootloader.bin

# Kernel
kernel: $(BUILD_DIR)/kernel.bin
$(BUILD_DIR)/kernel.bin:
	$(ASM) $(SRC_DIR)/kernel/main.asm -f bin -o $(BUILD_DIR)/kernel.bin
```

Targets:
- `ASM=nasm`: Defines the assembler as `nasm`;
- `SRC_DIR=src`: Specifies the source directory;
- `BUILD_DIR=build`: Specifies the build directory;

Building the Boot Disk Image:
- `floppy_image`: Target to create the boot disk image;
- `$(BUILD_DIR)/main.img`: Dependency indicating that `main.img` depends on the bootloader and kernel;

Bootloader Compilation:
- `bootloader`: Target to compile the bootloader;
- `$(BUILD_DIR)/bootloader.bin`: Dependency indicating that `bootloader.bin` depends on the bootloader source code;

Kernel Compilation:
- `kernel`: Target to compile the kernel;
- `$(BUILD_DIR)/kernel.bin`: Dependency indicating that `kernel.bin` depends on the kernel source code;

Commands:
- `dd if=/dev/zero of=$(BUILD_DIR)/main.img bs=512 count=2880`: Creates a blank disk image (`main.img`) with a size of 1.44 MB (2880 blocks of 512 bytes each);
- `mkfs.fat -F 12 -n "FAT12" $(BUILD_DIR)/main.img`: Formats the disk image with FAT12 file system and assigns the volume label "FAT12";
- `dd if=$(BUILD_DIR)/bootloader.bin of=$(BUILD_DIR)/main.img conv=notrunc`: Copies the compiled bootloader to the disk image without truncating existing data;
- `mcopy -i $(BUILD_DIR)/main.img $(BUILD_DIR)/kernel.bin "::kernel.bin"`: Copies the compiled kernel to the disk image with the destination path "::kernel.bin";

{: .important-title }
If I try to compile and run the code, I'll encounter an error `Bad target ::kernel.bin`. This error occurs because fat12 expects a header on the disk for proper initialization.

----

## **Header Structure**

The header contains essential information about the disk, such as the number of sectors, bytes per sector, and other disk-related details.

```
org 0x7c00
bits 16

jmp short main
nop

bdb_eom:                    db 'MSWIN4.1'
bdb_bytes_per_sector:       dw 512
bdb_sectors_per_cluster:    db 1
bdb_reserved_sectors:       dw 1
bdb_fat_count:              db 2
bdb_dir_entries_count:      dw 0e0h
bdb_total_sectors:          dw 2880
bdb_media_descriptor_type:  db 0f0h
bdb_sectors_per_fat:        dw 9
bdb_sectors_per_track:      dw 18
bdb_heads:                  dw 2
bdb_hidden_sectors:         dd 0
bdb_large_sector_count:     dd 0

ebr_drive_number:           db 0
                            db 0
ebr_signature:              db 29h
ebr_volume_id:              dd 12h,34h,56h,78h
ebr_volume_label:           db 'FAT12      '
ebr_system_id:              db 'FAT12   '

...rest of the previous project code...
```

- `jmp short main`: Jumps the header to the main code;
- `nop`: No operation, a placeholder for the first instruction;

The **header** structure includes the following fields, which are standard for a FAT12 disk:
- `bdb_eom`: End of message, 'MSWIN4.1';
- `bdb_bytes_per_sector`: Number of bytes per sector;
- `bdb_sectors_per_cluster`: Number of sectors per cluster;
- `bdb_reserved_sectors`: Number of reserved sectors;
- `bdb_fat_count`: Number of FATs (File Allocation Tables);
- `bdb_dir_entries_count`: Number of directory entries;
- `bdb_total_sectors`: Total number of sectors;
- `bdb_media_descriptor_type`: Media descriptor type;
- `bdb_sectors_per_fat`: Number of sectors per FAT;
- `bdb_sectors_per_track`: Number of sectors per track;
- `bdb_heads`: Number of heads;
- `bdb_hidden_sectors`: Number of hidden sectors;
- `bdb_large_sector_count`: Large sector count;
- `ebr_drive_number`: Drive number;
- `ebr_signature`: Signature;
- `ebr_volume_id`: Volume ID;
- `ebr_volume_label`: Volume label 11 bytes long;
- `ebr_system_id`: System ID 8 bytes long;

{: .important-title }
If I wanna see this structure, I can create a fat12 disk image and take a look inside with **hex editor** and see with more detail. For example, **jeex** or **wxHexEditor**.

----

## **INT 13 - Disk BIOS Services**

[INT 13](https://stanislavs.org/helppc/int_13.html), also known as **Diskette BIOS Services**, is a set of BIOS interrupts used for disk operations, particularly on floppy disks. These services provide a standardized interface for interacting with floppy disk drives at a low level.

Here's a brief overview of some common functions provided by **INT 13**:

1. **Read Sector**: Reads a specified sector from the disk into memory.
2. **Write Sector**: Writes data from memory to a specified sector on the disk.
3. **Verify Sector**: Verifies the contents of a specified sector on the disk.
4. **Format Track**: Formats a track on the disk with a specified format.
5. **Get Drive Parameters**: Retrieves information about the disk drive, such as the number of tracks, sectors per track, and bytes per sector.
6. **Reset Disk System**: Resets the disk drive to a known state.

These services are typically accessed by invoking **INT 13** with a specific function number and passing necessary parameters via registers or memory. The BIOS then performs the requested operation on the disk drive.

{: .important-title }
While **INT 13** was originally designed for floppy disks, it's also used for accessing hard disks in older systems. However, with the advent of more advanced disk interfaces and operating systems, direct use of **INT 13** has become less common, replaced by higher-level disk access APIs provided by the operating system or disk controller drivers.