---
title: Logical Operators
nav_order: 2
layout: default
parent: Operations
grand_parent: 🔲 x86 Assembly NASM
---

## **LOGICAL OPERATORS**

| Operator | Description | Result |
|:---------|:------------|:-------|
| `and`    | Logical AND  | `1` if both bits are `1`, otherwise `0` |
| `or`     | Logical OR   | `1` if either bit is `1`, otherwise `0` |
| `not`    | Logical NOT  | Inverts the bits of the operand |
| `xor`    | Logical XOR  | `1` if the bits are different, otherwise `0` |

----

### **AND Operation**

The `and` instruction is used to perform **logical AND** operations. If both bits are `1`, the result is `1`; otherwise, it's `0`.

```
section .data

section .text
    global _start

_start:
    mov eax, 0b1010  ; Load binary value 1010 into eax
    mov ebx, 0b1100  ; Load binary value 1100 into ebx
    and eax, ebx     ; Perform logical AND operation
```


```
eax = 0b1010 = 10
ebx = 0b1100 = 12
------------
eax = 0b1000 = 8
```

{: .important-title }
I used binary values because it's easier to understand with logical operators. This instruction performs a **bitwise AND** operation between the values in `eax` and `ebx`, storing the result in `eax`. The result of this operation is `0b1000`.

----

### **OR Operation**

The `or` instruction is used to perform **logical OR** operations. If either bit is `1`, the result is `1` otherwise, it's `0`.

```
section .data

section .text
    global _start

_start:
    mov eax, 0b1010  ; Load binary value 1010 into eax
    mov ebx, 0b1100  ; Load binary value 1100 into ebx
    or eax, ebx      ; Perform logical OR operation
```

```
eax = 0b1010 = 10
ebx = 0b1100 = 12
------------
eax = 0b1110 = 14
```

{: .important-title }
This instruction performs a **bitwise OR** operation between the values in `eax` and `ebx`, storing the result in `eax`. The result of this operation is `0b1110`.

----

### **NOT Operation**

The `not` instruction is used to perform **logical NOT** operations. It **inverts the bits** of the operand.

```
section .data

section .text
    global _start

_start:
    mov eax, 0b1010  ; Load binary value 1010 into eax
    not eax          ; Perform logical NOT operation
```

```
eax = 0b1010 = 10
------------
eax = 0b0101 = 5
```

{: .important-title }
This instruction performs a **bitwise NOT** operation on the value in `eax`, storing the result in `eax`. The result of this operation is `0b0101`.

One important thing about the `not` instruction is that it **inverts all the bits of the operand**, which may not be what I expected.

```
eax = 0b1010 0000 0000 0000 0000 0000 0000 0000
-----------------------------------------------
eax = 0b0101 1111 1111 1111 1111 1111 1111 1111
```

To avoid this, I can **mask the upper bits** to focus on the lower bits.

```
section .data

section .text
    global _start

_start:
    mov eax, 0b1010
    not eax
    AND eax, 0x0000000F ; Mask the upper 28 bits
                        ; can also use 0xF
```

{: .important-title }
In this case, I used the `and` instruction to **mask the upper 28 bits** of the result. This way, I can **ignore the upper bits** and focus on the lower 4 bits, which is the result of the `not` operation.

----

### **XOR Operation**

The `xor` instruction is used to perform **logical XOR** operations. If the bits are different, the result is `1` otherwise, it's `0`.

```
section .data

section .text
    global _start

_start:
    mov eax, 0b1010  ; Load binary value 1010 into eax
    mov ebx, 0b1100  ; Load binary value 1100 into ebx
    xor eax, ebx     ; Perform logical XOR operation
```

```
eax = 0b1010 = 10
ebx = 0b1100 = 12
------------
eax = 0b0110 = 6
```

{: .important-title }
This instruction performs a **bitwise XOR** operation between the values in `eax` and `ebx`, storing the result in `eax`. The result of this operation is `0b0110`.