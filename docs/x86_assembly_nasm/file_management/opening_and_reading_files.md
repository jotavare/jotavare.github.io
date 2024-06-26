---
title: Opening and Reading Files
nav_order: 1
layout: default
parent: File Management
grand_parent: 🔲 x86 Assembly NASM
---

## **OPENING AND READING FILES**

### **x86 System Call Table**

Before diving into code implementation, let's understand the **system calls** required.

| %eax | Name      | Source                     | %ebx             | %ecx              | %edx    | %esx | %edi |
|:-----|:----------|:---------------------------|:-----------------|:------------------|:--------|:-----|:-----|
| 1    | sys_exit  | kernel/exit.c              | int              | -                 | -       | -    | -    |
| 2    | sys_fork  | arch/i386/kernel/process.c | struct pt_regs   | -                 | -       | -    | -    |
| 3    | sys_read  | fs/read_write.c            | unsigned int     | char *            | size_t  | -    | -    |
| 4    | sys_write | fs/read_write.c            | unsigned int     | const char *      | size_t  | -    | -    |
| 5    | sys_open  | fs/open.c                  | const char *     | int               | int     | -    | -    |
| ...  | ...       | ...                        | ...              | ...               | ...     | ...  | ...  |

I'll focus on the `open` and `read` system calls for file manipulation.

{: .important-title }
I can find the complete x86 system call table [here](https://faculty.nps.edu/cseagle/assembly/sys_call.html), [here](https://chromium.googlesource.com/chromiumos/docs/+/master/constants/syscalls.md), or [here](https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/). Additionally, I can use the terminal command `man syscalls` to access the system call manual.

----

### **Opening a File**

If I use the terminal command `man 2 open` (also [here](https://man7.org/linux/man-pages/man2/open.2.html)), I'll find the following function:

```c
int open(const char *pathname, int flags);
```

So, I need the following information to open a file:
- `open` system call requires `eax` to be set to `5`;
- It takes a **file path** on `ebx` as a `const char *`;
- I need to provide a **flag** as an argument to `ecx`;

{: .important-title }
Flags are used to **specify the mode** in which the file should be opened. For example, `O_RDONLY` for **read-only mode**, `O_WRONLY` for **write-only mode**, and `O_RDWR` for **read-write mode**. I can check that in the terminal using `man 2 open` and scrolling down to the `flags` section.

One small thing is that in `man`, the flags are defined as `C macros`, but in assembly, I need to use the **actual values**. I can go to the [fcntl.h](https://sites.uclouvain.be/SystInfo/usr/include/asm-generic/fcntl.h.html) file and find the actual value of `O_RDONLY` which is `00000000 = 0`.

```
section .data
    pathname db "path/to/file.txt"

section .text
    global main

main:
    mov eax, 5
    mov ebx, pathname
    mov ecx, 0
    int 80h
```

- The result of the system call will be my **file descriptor**, which will be stored in `eax`;
- I can use in **GDB** `x/10x [pointer]` to see the memory content (hexadecimal format) and  `x/10s [pointer]` (string format);

{: .important-title }
A **file descriptor** is a unique identifier assigned by the operating system to a file when it is opened. It is used to reference the file in subsequent operations. The first three file descriptors are reserved for **standard input**, **output**, and **error streams** (`0`, `1`, and `2`, respectively). The file descriptor returned by the `open` system call will be a **positive integer greater** than `2`.

----

### **Reading from the File**

If I use the terminal command `man 2 read` (also [here](https://man7.org/linux/man-pages/man2/read.2.html)), I'll find the following function:

```c
ssize_t read(int fd, void *buf, size_t count);
```

{: .important-title}
Since I now know the file descriptor from the previous example `eax = 3`, I can now read from the file using the `read` system call.

So, I need the following information to `read` from a file:
- It copies `eax` to `ebx` to use the **file descriptor**;
- I will need a **buffer** to store the data read from the file;
- The **size** of the buffer should be provided to `edx` as a `size_t`;

```
section .data
    pathname db "path/to/file.txt"

section .bss
    buffer resb 1024    ; Reserve 1024 bytes for the buffer because I don't know the file size

section .text
    global main

main:
    mov eax, 5          ; Open system call
    mov ebx, pathname   ; File path
    mov ecx, 0          ; Flags
    int 80h             ; Call the system

    mov ebx, eax        ; Store the file descriptor in ebx
    mov eax, 3          ; Read system call
    mov ecx, buffer     ; Buffer to store the data
    mov edx, 1024       ; Size of the buffer
    int 80h             ; Call the system

    mov eax, 1          ; Exit system call
    mov ebx, 0          ; Exit code (success)
    int 80h             ; Call the system
```

{: .important-title}
The result of the system call will be the **number of bytes read**, which will be stored in `eax`. If `eax` is `0`, it means that the **end of the file** has been reached. If `eax` is `-1`, it means that an **error occurred**. If `eax` is `-2`, it means that the file descriptor is **invalid**.