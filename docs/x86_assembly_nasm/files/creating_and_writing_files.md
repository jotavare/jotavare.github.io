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

I need to combine flags together using the `or` operator. For example, `101o` is equivalent to `O_CREAT | O_WRONLY | O_TRUNC`. I can set the flags individually and combine them using the `or` operator or use the combined value directly.

{: .important-title }
Visual Studio Code usually **shows the value** if you hover over the flag.

```
    O_CREAT  = 0100
    O_WRONLY = 0001
 or ---------------
               0101
```

The way we declare `0101` in octal is `101o`. We can exclude the leading zeros.

{: .important-title }
When combining multiple flags using bitwise `or`, as shown in the assembly code, the resulting combination may be represented in octal format for specifying file permissions and behavior. In assembly language, octal literals are often denoted by appending a lowercase "o" to the number, such as `101o` in the provided code snippet. This notation indicates that the number is in octal format.

----

### **File Permissions**

File permissions are represented in octal format as follows:

```
    S_IRUSR = 0400
    S_IWUSR = 0200
    S_IXUSR = 0100
 or --------------
              0700
```

{: .important-title }
To sum it up, `or` is basically adding the values together. I can also check these values in [stat.h](https://man7.org/linux/man-pages/man0/sys_stat.h.0p.html) file.

----

Your guide is now well-organized and concise! Let me know if you need further adjustments or assistance.

### **Open/Create File**

- `eax` register with the value `5` to indicate the `open` syscall;
- `ebx` register with the file path;
- `ecx` register with the value `101o` for flags like `ocreate` and `write`;
- `edx` register with the value `0700o` for permissions like `rwxr--r-`;
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