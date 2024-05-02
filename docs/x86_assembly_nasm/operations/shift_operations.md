---
title: Shift Operations
nav_order: 3
layout: default
parent: Operations
grand_parent: 🔲 x86 Assembly NASM
---

## **SHIFT OPERATIONS**

{: .important-title }
I already knew this in `C`, which is called **bitwise shifting**. It's a **fast way** to multiply or divide by **powers of 2**. For example, shifting a number to the left by `1` is equivalent to multiplying it by `2`. Similarly, shifting a number to the right by `1` is equivalent to dividing it by `2`.

| Operator | Description | Result |
|:--------:|:-----------:|:------:|
| `shr`    | Logical Right Shift | Shifts the bits to the right |
| `shl`    | Logical Left Shift  | Shifts the bits to the left |
| `sar`    | Arithmetic Right Shift | Shifts the bits to the right, preserving the sign bit |
| `sal`    | Arithmetic Left Shift  | Shifts the bits to the left, preserving the sign bit |

### **SHR Operation**

The `shr` instruction is used to perform **logical right shift** operations. It shifts the bits of the operand to the **right** by a specified number of bits.

```
section .text
    .global _start
_start:
        move eax, 2 ; 0010 = 2
        shr eax, 1  ; shift the bits to the right one spot -> 0001 = 1
                    ; this equivelent to dividing by 2 but it's faster
```

----

### **SHL Operation**

The `shl` instruction is used to perform **logical left shift** operations. It shifts the bits of the operand to the **left** by a specified number of bits.

```
section .text
    .global _start

_start:
        move eax, 2 ; 0010 = 2
        shl eax, 1  ; shift the bits to the left one spot -> 0100 = 4
                    ; this equivelent to multiplying by 2 but it's faster
```

----

### **SAR Operation**

The `sar` instruction is used to perform **arithmetic right shift** operations. It shifts the bits of the operand to the **right** by a specified number of bits, while **preserving the sign bit**.

```
section .text
    .global _start

_start:
        move eax, -2 ; 1110 = -2
        sar eax, 1  ; shift the bits to the right one spot -> 1111 = -1
                    ; this equivelent to dividing by 2 but it's faster
```

----

### **SAL Operation**

The `sal` instruction is used to perform **arithmetic left shift** operations. It shifts the bits of the operand to the **left** by a specified number of bits, while **preserving the sign bit**.

```
section .text
    .global _start

_start:
        move eax, -2 ; 1110 = -2
        sal eax, 1  ; shift the bits to the left one spot -> 1100 = -4
                    ; this equivelent to multiplying by 2 but it's faster
```


