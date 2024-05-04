---
title: Calling C Functions
nav_order: 1
layout: default
parent: Procedures and Functions
grand_parent: 🔲 x86 Assembly NASM
---

## **CALLING C FUNCTIONS**

### **C Function Definition**

When writing assembly code, I can **call standard C functions** like `printf` and `exit` using the `gcc` compiler but first I need a **few changes** in the code:

```
extern printf
extern exit

section .data
	msg db "Hello World!", 0
	msg1 db "Another Hello!", 0
	fmt db "Output is: %s %s",10,0

section .text
    global main

main:
	push msg
	push fmt
	call printf
	push 1
	call exit
```

- `extern` is used to tell the assembler that the **function is defined elsewhere**;
- `printf` and `exit` are functions that are defined in the **C standard library**;
- Instead of `global _start`, I use `global main` because the `gcc` compiler expects a `main`;
- `PUSH` is used to **push data into the stack**;
- `CALL` is used to **call a function**;

----

### **Stack Usage**

The stack is a **Last-In-First-Out (LIFO)** data structure, meaning the **last item pushed** onto the stack is the **first one to be popped off**. Picture it like stacking plates in a cafeteria tray, the last plate you put on top is the first one you'll take off when you need it.

Taking into account the previous example:
- My print function parameters are `printf(format, message)`;
- I first `PUSH msg` and then `PUSH fmt` onto the stack;

This order **might seem counterintuitive** at first because I usually think of passing arguments in the order they are listed. However, the arguments are **pushed in reverse order**, ensuring that the function receives them in the correct sequence.

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
- `-no-pie` flag is used to **disable** the **Position Independent Executable** feature;
- `-m32` flag specifies the target architecture as **32 bits for x86**;
- `-f` flag is used to specify the **input format**, in this case, `elf32`;

{:.important-title}
**Position Independent Executable (PIE)** is a feature that modern operating systems and compilers use to **randomize the base address of executables** in memory. This randomness helps to avoid **security attacks** like buffer overflow by making it difficult for attackers to predict memory layouts. However, in some cases, **fixed addresses** may be needed for **compatibility** or **performance reasons**.