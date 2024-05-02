---
title: Floating Point Numbers
nav_order: 6
layout: default
parent: Operations
grand_parent: 🔲 x86 Assembly NASM
---

## **FLOATING POINT NUMBERS**

### **Defining Floating Point Numbers**

To define floating-point numbers, we can use the `dd` directive in the data section to represent 32-bit floating-point values.

```
x dd 3.14
y dd 2.1
```

These lines define two floating-point numbers, `x` and `y`, with the respective values of 3.14 and 2.1.

----

### **Loading Values into Registers**

To load these values into registers, we utilize the `movss` instruction (`ss` **Scalar Single Precision Floating-Point Value**).

```
movss xmm0, [x]
movss xmm1, [y]
```

`xmm0` and `xmm1` are **special registers** designed for storing floating-point numbers (can use up to `xmm15`). The square brackets indicate fetching the value stored at the memory address of `x` and `y`, respectively.

----

## **Performing Operations**

Performing arithmetic operations like addition, subtraction, multiplication, and division follows similar principles.

```
addss xmm0, xmm1
```

This instruction adds the values stored in `xmm0` and `xmm1`, storing the result back into `xmm0`.

----

## **Precision Considerations**

One crucial consideration when working with **floating-point numbers is precision**. Floating-point values are stored using **IEEE floating-point notation**, which can lead to slight **inaccuracies** in representation. For example, `3.14` might be stored as `3.1400001` due to these limitations.

**IEEE** - In the `32 bit` **IEEE format**, `1 bit` is allocated as the **sign bit**, the next **8 bits** are allocated as the **exponent field**, and the **last 23 bits** are the **fractional parts** of the normalized number. A **sign bit** of `0` indicates a **positive number**, and a `1` is **negative**.

```
section .data
    x DD 3.14
    y DD 2.1

section .text

global _start

_start:
        movss xmm0, [x] ; scalar single precision floating point move
                        ; scalar because we are moving a single decimal value
                        ; single precision meaning is a 32-bit floating point number
        
        movss xmm1, [y]
        addss xmm0, xmm1
        mov ebx, 1
        int 80h

        ; xmm0 = 3.1400001 IEEE
        ; xmm1 = 2.0999999 IEEE
        ; result = 5.2399977 IEEE
```

{: .important-title }
To print the value of `xmm0` in GDB, use the command `p $xmm0.v4_float[0]`.

----

## **Compare Floating Point Numbers**

Comparing floating-point numbers is a bit more complex than comparing integers. The `cmp` instruction doesn't work with floating-point numbers, so we use the `ucomiss` instruction instead.

```
section .data
    x DD 3.14
    y DD 2.1

section .text

global _start

_start:
        movss xmm0, [x]
        movss xmm1, [y]
        ucomiss xmm0, xmm1  ; cmp doesn't work
        ja above            ; jump if above
        jmp end

above:
        mov ecx, 1

end:
        mov eax, 1
        mov ebx, 1
        int 80h
```

{: .important-title }
Also, `ja` (jump above) instead of `jg` (jump greater) because we are comparing floating point numbers. The only jump condition equal to integers is `je` (jump equal). The rest is as follows: `jb` (jump below), `jae` (jump above or equal), `jbe` (jump below or equal), `jne` (jump not equal).
