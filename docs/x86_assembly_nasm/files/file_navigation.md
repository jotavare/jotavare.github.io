---
title: File Navigation
nav_order: 2
layout: default
parent: Files
grand_parent: 🔲 x86 Assembly NASM
---

## **FILE NAVIGATION**

## **Introduction to lseek**

The **lseek** system call facilitates efficient **file navigation** within an open file in x86 assembly. It allows us to move to specific positions within a file, essentially for scenarios like **fixed-size record** processing.

Let's use this file `text.txt` example:
```bash
001, 15, 20
002, 25, 30
003, 30, 50
004, 60, 80
005, 90, 43
006, 10, 10
```

{: .important-title }
While each record appears to be **nine characters long**, it's crucial to recognize that **newline characters** add an additional **byte**, making each record **ten bytes** in total.

----

### **Implementation Overview**

If I use the terminal command `man 2 lseek` (also [here](https://man7.org/linux/man-pages/man2/lseek.2.html)), I'll find the following function:

```c
off_t lseek(int fd, off_t offset, int whence);
```

So, I need the following information to open a file:
- `lseek` system call requires `eax` to be set to `19`, check [here](https://faculty.nps.edu/cseagle/assembly/sys_call.html);
- It takes the **file descriptor** on `ebx` which is `3`;
- The **offset** in bytes to move the file pointer is provided to `ecx`;
- The **whence** parameter specifies the **starting point** for the offset in `edx`;

Just like `0_RDONLY`, the `SEEK_SET`, `SEEK_CUR`, and `SEEK_END` are **C macros** defined in the `unistd.h` file. I can find the actual values in the [unistd.h](https://sites.uclouvain.be/SystInfo/usr/include/asm-generic/unistd.h.html) which are `0`, `1`, and `2` respectively.

{: .important-title }
In this example, I'm using `SEEK_SET` which means the offset is relative to the **beginning of the file**, `SEEK_CUR` is relative to the **current file position**, and `SEEK_END` is relative to the **end of the file**.

```
section .data
    pathname db "path/to/file.txt"

section .bss
    buffer resb 10

section .text
    global main

main:
    mov eax, 5          ; open syscall
    mov ebx, pathname   ; file path
    mov ecx, 0          ; read only
    int 80h
    
    mov ebx, eax
    mov eax, 19         ; lseek syscall
    mov ecx, 20         ; bytes to offset
    mov edx, 0          ; offset from beginning of file SEEK_SET
    int 80h

    mov eax, 3          ; read syscall
    mov ecx, buffer     ; buffer to read into
    mov edx, 10         ; read 10 bytes
    int 80h

    mov eax, 1
    mov ebx, 0
    int 80h
```

- The **result** of the `lseek` system call will be the **new file offset**;
- **GDB** `x/10x [pointer]` to see the memory content **(hexadecimal format)**;
- **GDB**  `x/10s [pointer]` to see the memory content **(string format)**;
- The **buffer** will contain the **first record** from the file;
- The **file offset** will be at the **beginning** of the file;