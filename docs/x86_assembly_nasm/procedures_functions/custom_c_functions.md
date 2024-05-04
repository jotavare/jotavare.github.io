---
title: Custom C Functions
nav_order: 2
layout: default
parent: Procedures and Functions
grand_parent: 🔲 x86 Assembly NASM
---

## **CUSTOM C FUNCTIONS**

### **Custom C Function Definition**

In this example, I have a `C` file named `sum.c` with a function named `sum` and a assembly file:

```c
#include <stdio.h>

extern int sum(int a, int b);

int sum(int a, int b)
{
    printf("Here!\n");
    return (a + b);
}
```

```
extern sum
extern exit

section .text
    global main

main:
    push 1
    push 2
    call sum
    push eax
    call exit
```

{:.important-title}
- `extern` is used to tell the assembler that the **function is defined elsewhere**;
- I use the `call` instruction to call my custom function `sum` from the `sum.c` file;
- The `eax` register contains the return value of the function;

----

### **Compilation Process**

Now I can compile and link my **assembly code** with my file `sum.c`.

<div class="code-example" markdown="1">
First, generate the **object file** using `nasm`. Second, compile the `sum.c` file and **link it with the object file**.
</div>
```bash
nasm -f elf32 -o first.o first.s
gcc -m32 -o first first.o sum.c -no-pie
```