---
title: Creating and Writing Files
nav_order: 3
layout: default
parent: Files
grand_parent: 🔲 x86 Assembly NASM
---

## **CREATING AND WRITING FILES**

### **Code Example**

```
section .data
    pathname db "path/to/file.txt"
    msg db "Hello, World!", 0AH,0DH, "$"

section .text
    global main

main:
    ; open file
    mov eax, 5
    mov ebx, pathname

    ; create file if it doesn't exist
    mov ecx, 101o
    mov edx, 0700o
    int 80h

    ; write to file
    mov ebx, eax
    mov eax, 4
    mov ecx, msg
    mov edx, 16

    ; exit program
    mov eax, 1
    mov ebx, 0
    int 80h
```

----

### **Create and Read Flags**

I need to combine flags together using the `or` operator or use the **combined value directly**. For example, `101o` is equivalent to `O_CREAT | O_WRONLY`.

```
    O_CREAT  = 0100
    O_WRONLY = 0001
 or ---------------
               0101
```

The way I declare `0101` in octal:
- Exclude the leading zero `101`;
- Append a lowercase `o` to the number `101o` to indicate octal format;

{: .important-title }
Visual Studio Code usually **shows the value directly** if I hover over the flag or I can check these values directly in [stat.h](https://man7.org/linux/man-pages/man0/sys_stat.h.0p.html).

----

### **File Permission Flags**

```
    S_IRUSR = 0400
    S_IWUSR = 0200
    S_IXUSR = 0100
 or --------------
              0700
```

- `S_IRUSR` is the **read** permission for the owner;
- `S_IWUSR` is the **write** permission for the owner;
- `S_IXUSR` is the **execute** permission for the owner;
- `0700` is the combination of these permissions;

{: .important-title }
To sum it up, `or` is basically **adding** the values together. 

----

### **Open/Create File**

- `eax` register with the value `5` to indicate the `open` syscall;
- `ebx` register with the file path;
- `ecx` register with the value `101o` for flags `create` and `write`;
- `edx` register with the value `0700o` for permissions like `rwx`;
- `int 80h` to invoke the syscall;

----

### **Write to File**

- `eax` register with the value `4` to indicate the `write` syscall;
- `ebx` register with the file descriptor `eax` obtained from the `open` syscall;
- `ecx` register with the data to be written `msg`;
- `edx` register with the size of the data to write `16`;

----

### **Exit Program**
- `eax` register with the value `1` to indicate the `exit` syscall;
- `ebx` register with the value `0` to indicate successful execution;