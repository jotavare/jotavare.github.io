---
title: First Program
nav_order: 2
layout: default
parent: Projects
grand_parent: 🔲 x86 Assembly NASM
---

## **BUILDING A SIMPLE BOOTLOADER**

### **Bootloader Process**

Bootloaders are programs responsible for **initializing hardware** and **starting the operating system**. 

When a computer boots in **legacy mode**, the following sequence occurs:

1. It enters the **BIOS (Basic Input Output System)**;
2. The **BIOS** initiates the boot process by accessing the boot sequence, which determines the order in which devices are checked for bootable code;
3. Each device in the boot sequence is accessed, and its first sector, known as the **MBR**, is loaded into memory at address `0x7c00`.
5. The BIOS checks for a signature `0aa55h` at the end of the `512 byte` sector loaded into memory at `0x7c00`, indicating a valid bootloader;
6. If the signature is found, the BIOS transfers control to the bootloader code at memory address `0x7c00`, initiating the execution of the bootloader;

{: .important-title }
In the context of traditional **x86 BIOS bootloaders**, the bootloader is typically `512 bytes` in size. This is because the **MBR**, which contains the bootloader code, occupies the first sector `512 bytes` of a storage device such as a hard disk or a floppy disk.

----

### **Project Structure**

- **Build Folder**: Files generated during the build process, `img` and `bin`;
- **Source Folder**: Source code for the bootloader, named `simple_bootloader.asm`;
- **Makefile**: This file automates the build process;

----

### **Writing the Bootloader**

To create the bootloader, follow these steps:

- Use `org` (origin) directive to set the origin address to `0x7c00`;
- Set the processor mode to 16 bits using `bits 16`;
- Use `hlt` to halt the CPU after execution;
- Create an infinite loop using `jmp halt` to ensure the CPU remains halted;
- Fill the remaining space in the `512 byte` sector with **zeros** using `times 510-($-$$) db 0`.
- Add the signature `dw 0aa55h` at the end of the bootloader.

```
org 0x7c00
bits 16

main:
    hlt

halt:
    jmp halt

    times 510-($-$$) db 0
    dw 0aa55h
```

{: .important-title }
`**org**` is used to specify the origin address or starting address for the code or data that follows it. In this case, I set the origin address to `0x7c00` to align with the memory location where the bootloader is loaded.

{: .important-title }
`16 bits` is the standard processor mode for bootloaders, ensuring **compatibility with legacy systems**. After that, depending on the operating system, the processor mode can be switched to `32` or `64 bits`.

----

### **Writing the Makefile**
To build the bootloader and automate the process, I need to create `**Makefile**`:

```makefile
# Assembler
**ASM=nasm**

# Directories
**SRC_DIR=src**
**BUILD_DIR=build**

# Targets
**$(BUILD_DIR)/main.img: $(BUILD_DIR)/main.bin**
**	cp $(BUILD_DIR)/main.bin $(BUILD_DIR)/main.img**
**	truncate -s 1440k $(BUILD_DIR)/main.img**

# Build
**$(BUILD_DIR)/main.bin: $(SRC_DIR)/main.asm**
**	$(ASM) $(SRC_DIR)/main.asm -f bin -o $(BUILD_DIR)/main.bin**
```

### **Running the Bootloader**
To test the bootloader, I use an emulator like **QEMU**:

```bash
qemu-system-i386 -fda build/main.img
```

{: .important-title }
**QEMU** is a popular emulator that can run **x86 operating systems**. I can also run the bootloader on real hardware by writing the image to a USB drive.