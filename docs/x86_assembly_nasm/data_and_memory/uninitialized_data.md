---
title: Uninitialized Data
nav_order: 6
layout: default
parent: Data and Memory
grand_parent: 🔲 x86 Assembly NASM
---

## **UNINITIALIZED DATA**

### **BSS Section**

In **x86 assembly**, sometimes I need to **reserve memory** for potential data storage without initializing it to specific values. This is where the **BSS section** comes into play.

```
section .bss
    num resb 3      ; Reserves three bytes of memory for 'num'

section .text
    global _start

_start:
    mov bl, 1       ; Move the value 1 into bl
    mov [num], bl   ; Move the value in bl into the memory space reserved for 'num'
    mov [num+1], bl ; Move the value in bl into the next byte of 'num'
    mov [num+2], bl ; Move the value in bl into the second next byte of 'num'

                    ; Exiting the program
    mov eax, 1      ; Move 1 to eax
    int 80h         ; Interrupt
```

{: .important-title }
In x86 assembly, **sizes are not inherently understood**, so I need to provide context for data manipulation. That's why I first move the value `1` into the `bl` register and then transfer it into the memory space reserved for `num`. To access a **specific byte** of `num`, I can utilize expressions like `[num+1]` or `[num+2]` to reference the subsequent bytes in memory.

----

### **Initializing Data (alternative)**

Alternatively, I can initialize data with default values using the `section .data`. Instead of manually reserving and setting values, I can use the `dup` instruction to initialize memory with the specified value.

```
section .data
    num2 db 3 dup (2) ; Initializes 'num2' with three instances of the value 2

section .text
    global _start

_start:
    mov bl, 1       ; Move the value 1 into bl
    mov [num2], bl  ; Move the value in bl into the memory space reserved for 'num2'

    mov [num], bl   ; Move the value in bl into the memory space reserved for 'num'
    mov [num+1], bl ; Move the value in bl into the next byte of 'num'
    mov [num+2], bl ; Move the value in bl into the second next byte of 'num'

                    ; Exiting the program
    mov eax, 1      ; Move 1 to eax
    int 80h         ; Interrupt
```