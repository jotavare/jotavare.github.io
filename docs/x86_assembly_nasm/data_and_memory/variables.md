---
title: Variables
nav_order: 4
layout: default
parent: Data and Memory
grand_parent: 🔲 x86 Assembly NASM
---
    
## **VARIABLES**

### **Declaration of Variables**
```
section .data
    num DB 1
    num2 DB 2

section .text
    global _start

_start:
    MOV bl,[num]
    MOV cl,[num2]
```
- Declared **one-byte** variable for `num` and `num2`, with initial values of `1` and `2` respectively.
- Loaded the values of the declared variables into the `bl` and `cl` registers, which represent the **lower 8 bits** of the `bx` and `cx` registers.

----

### **Efficient Memory Usage**
- x86 maximizes memory usage by storing **bytes next to each other**.
- Accessing a single byte from a memory slot, I will retrieve the **entire 32-bit** chunk it belongs to.
- Accessing these values directly can lead to **unexpected results** due to x86's memory efficiency.

----

### **Register Referencing**
- Removing the `e` (`ebx` -> `bx`) prefix slices the register in **16 bits**.
- Removing the `e` and `x` (`ebx` -> `bl` or `bh`) suffix references the **lower or higher 8-bit** parts.

----

### **High vs. Low Bits**
- By referencing the **lower 8 bits** of the registers, I ensure we're working with the **correct byte-sized data**.
- Setting high bits (`bh` or `ch`) affects the interpretation of the entire register.
- High bits are **interpreted differently** due to their **position in the binary representation**.