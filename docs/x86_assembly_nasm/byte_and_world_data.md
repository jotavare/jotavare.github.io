---
title: Byte and Word Data
nav_order: 7
layout: default
parent: 🔲 x86 Assembly NASM
---
    
## **BYTE AND WORD DATA**

## **Declaration of Variables**
```assembly
section .data
    num DB 1
    num2 DB 2

section .text
    global _start

_start:
    MOV bl,[num]
    MOV cl,[num2]
```
- Declared one-byte variable for `num` and `num2`, with initial values of 1 and 2 respectively.
- Loaded the values of the declared variables into the BL and CL registers, which represent the lower 8 bits of the `bx` and `cx` registers.

## **Efficient Memory Usage**
- x86 maximizes memory usage by storing **bytes next to each other**.
- Accessing a single byte from a memory slot, we retrieve the entire **32-bit** chunk it belongs to.
- Accessing these values directly can lead to **unexpected results** due to x86's memory efficiency.

## **Register Referencing**
- Removing the 'e' prefix slices the register in **16 bits** (e.g., `ax`, `bx`, `cx`, `dx`).
- Removing the 'x' suffix references the lower and higher **8-bit** parts (e.g., `al`, `ah`, `bl`, `bh`).

## **High vs. Low Bits**
- By referencing the **lower 8 bits** of the registers, we ensure we're working with the **correct byte-sized data**.
- Setting high bits (`bh` or `ch`) affects the interpretation of the entire register.
- High bits are interpreted differently due to their position in the binary representation.