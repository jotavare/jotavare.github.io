---
title: Loops
nav_order: 5
layout: default
parent: Operations
grand_parent: 🔲 x86 Assembly NASM
---

## **LOOPS**

Loops are used to execute a block of code **multiple times**. They are essential for repetitive tasks and are widely used in programming.

```
section .data
    list DB 1,2,3,4

section .text

global _start

_start:
    mov eax, 0
    mov cl, 0

loop:
    mov bl,[list + eax]
    add cl, bl
    inc eax     ; eax = eax + 1 ... can also do add eax, 1
    cmp eax, 4  ; can aslo do cmp [list + eax], 4
    JE end
    JMP loop

end:
    mov eax, 1  ; Set eax to 1, indicating the exit system call
    mov ebx, 1  ; Set ebx to 1, indicating a normal program termination
    int 80h     ; Invoke the system call
```

{: .important-title }
In the end, `eax` and `ebx` are set to `1`, to indicate a **normal program termination**. The `int 80h` instruction invokes the system call to exit the program. This example demonstrates a **simple loop** that iterates over an array of numbers and **calculates their sum**. The loop continues until the **end of the array is reached**. In this case I know the array has `4` elements and that the end of the array is `4` but in future programs I should **calculate the length of the array** dynamically and use a better **null terminator**, like `-1` or `0`.
