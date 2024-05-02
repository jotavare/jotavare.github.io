---
title: ARITHMETIC OPERATIONS
nav_order: 10
layout: default
parent: Data and Memory
grand_parent: 🔲 x86 Assembly NASM
---

## **ARITHMETIC OPERATIONS**

### **ADD Operation**

The `add` instruction is used to perform addition operations in x86 assembly. Here's an example:

```
section .data

section .text
    global _start

_start:
    mov eax, 2      ; Load value 5 into eax
    mov ebx, 3      ; Load value 3 into ebx
    add eax, ebx    ; Add ebx to eax
```

{: .important-title }
This instruction adds the value in `ebx` to `eax` and stores the result in `eax`. So, after this operation, `eax` should contain the **sum of the two numbers** `5`. Also, we can represent a number like `2` in binary as `0b00000010` and in hexadecimal as `0x02`.

### Handling Carry Flag (CF)

The Carry Flag `CF` is another crucial aspect, especially when dealing with arithmetic operations involving limited register sizes. Consider a scenario where the result exceeds the capacity of the destination register.

```
section .data

section .text
    global _start

_start:
    mov al, 0xFF    ; Load value 255 into al
    mov bl, 1       ; Load value 1 into bl
    add al, bl       ; Add 1 to al
```

{: .important-title }
In this case, the result of the addition operation is `256`, which is too large to fit into the `al` register. In such cases, the extra bits are carried over and stored in the `CF` of the E-Flags register. We can utilize the `ADC` (Add with Carry) instruction to incorporate this carry into subsequent operations.

### **ADC Operation**

The `adc` instruction is used to perform addition operations with a carry in x86 assembly.

```
section .data

section .text
    global _start

_start:
    mov al, 0xFF    ; Load value 255 into al
    mov bl, 1       ; Load value 1 into bl
    add al, bl      ; Add 1 to al
    adc al, 0       ; Add the carry flag to the result
```

{: .important-title }
In this case, the `adc` instruction adds the value in the carry flag to the result of the previous addition operation. This allows us to handle scenarios where the result exceeds the capacity of the destination register and carry over the extra bits.

### **SUB Operation**

The `sub` instruction is used to perform subtraction operations in x86 assembly.

```
section .data

section .text
    global _start

_start:
    mov al, 5       ; Load value 5 into al
    mov bl, 3       ; Load value 3 into bl
    sub al, bl      ; Subtract 3 from 5
```

{: .important-title }
This instruction subtracts the value in `bl` from `al` and stores the result in `al`. So, after this operation, `al` should contain the **difference of the two numbers** `2`.

Now lets flip the numbers and see what happens:

```
section .data

section .text
    global _start

_start:
    mov al, 3       ; Load value 3 into al
    mov bl, 5       ; Load value 5 into bl
    sub al, bl      ; Subtract 5 from 3
```

{: .important-title }
In this case, the result of the subtraction operation is `-2`, which is a negative number. The `SF` (Sign Flag) in the E-Flags register will be set to `1` to indicate that the result is negative.

Another example, what if we move to ebx the number 2 and add to eax:

```
section .data

section .text
    global _start

_start:
    mov eax, 3      ; Load value 5 into eax
    mov ebx, 5      ; Load value 2 into ebx
    sub eax, ebx    ; Subtract 2 from 5
    mov ebx, 2      ; Load value 2 into ebx
    add eax, ebx    ; Add -2 to 2
```

{: .important-title }
