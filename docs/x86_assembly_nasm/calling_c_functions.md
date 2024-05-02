---
title: Calling C Functions
nav_order: 8
layout: default
parent: 🔲 x86 Assembly NASM
---

## **CALLING C FUNCTIONS**

### **C Function Definition**

When writing assembly code, I can **call standard C functions** like `printf` and `exit` using the `gcc` compiler but first I need a **few changes** in the assembly code:

```
extern printf  ; printf(format, message)
extern exit    ; exit(1)
               ; this tells nasm that this function are gonna be linked later

section .data
	msg DD "Hello World!", 0        ; DD = Define Double Word = 32 bits = 4 bytes
	msg DD "Hello World!", 0        ; 0 = null character
	fmt DB "Output is: %s %s",10,0  ; DB = Define Byte = 8 bits = 1 byte
                                    ; 10 = new line
                                    ; 0 = null character

section .text

global main     ; this is because we need a main function in order to work with gcc

main:
	PUSH msg    ; take the data and push to the end of the stack
	PUSH fmt    ; the order is important
	CALL printf ; call the function
	PUSH 1      ; push to the stack
	CALL exit   ; call the exit function with the exit code (1)
```

- `extern` is used to tell the assembler that the **function is defined elsewhere**.
- `printf` and `exit` are functions that are defined in the **C standard library**.
- Instead of `global _start`, I need to use `global main` because the `gcc` compiler expects a `main` function.
- `PUSH` is used to **push data into the stack**.
- `CALL` is used to **call a function**.

----

### **Stack Usage**

The stack is a **Last-In-First-Out (LIFO)** data structure, meaning the **last item pushed** onto the stack is the **first one to be popped off**. Picture it like stacking plates in a cafeteria tray: the last plate you put on top is the first one you'll take off when you need it.

Let's take a look at the previous example, `printf` parameters are `printf(format, message)`. In my code, I first `PUSH msg` and then `PUSH fmt` onto the stack. This order **might seem counterintuitive** at first because we usually think of passing arguments in the order they are listed. However, the arguments are **pushed in reverse order**, ensuring that the function receives them in the correct sequence.

----

### **Compiling with GCC**

<div class="code-example" markdown="1">
Generate the **object file** using `nasm` and **compile the final binary** using `gcc`:
</div>
```
nasm -f elf32 -o program_name.o program_name.s
gcc -no-pie -m32 -o program_name program_name.o 
```

{:.important-title}
- `-no-pie` flag is used to **disable** the **Position Independent Executable** feature.
- `-m32` flag specifies the target architecture as **32 bits for x86**.
- `-f` flag is used to specify the **output format**, in this case, `elf32`.

{:.important-title}
**Position Independent Executable (PIE)** is a feature that modern operating systems and compilers use to **randomize the base address of executables** in memory. This randomness helps to avoid **security attacks** like buffer overflow by making it difficult for attackers to predict memory layouts. However, in some cases, **fixed addresses** may be needed for **compatibility** or **performance reasons**.

----

### **Custom C Function Definition**

In this example, I have a `C` file named `sum.c` with a function named `sum`:

```c
#include <stdio.h>

extern int sum(int a, int b);

int sum(int a, int b) {
    printf("Here!\n");
    return (a + b);
}
```

- We declare this function as `extern` to make it accessible to our assembly program.

----

### **Calling Custom C Functions**

```
extern sum
extern exit

section .data
section .text

global main

main:
    PUSH 1      ; second argument
    PUSH 2      ; first argument
    CALL sum    ; call the function
    PUSH eax    ; push the result from sum to the stack
    CALL exit   ; exit the program
```

{:.important-title}
- I use the `call` instruction to call my custum `C` function `sum`.
- The `eax` register contains the return value of the function.

----

### **Compilation Process**

To compile and link our assembly code with our `C` file `sum.c`, follow these steps:

<div class="code-example" markdown="1">
Generate the **object file** using `nasm` and compile the `C` file and **link it with the object file**:
</div>
```bash
nasm -f elf32 -o first.o first.s
gcc -m32 -o first first.o sum.c -no-pie
```