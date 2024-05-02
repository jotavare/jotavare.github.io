---
title: Comparison and Jumps
nav_order: 4
layout: default
parent: Operations
grand_parent: 🔲 x86 Assembly NASM
---

## **COMPARISON AND JUMPS**

{: .important-title }
In `C`, we use **conditional statements** to make decisions based on the value of a variable. In assembly, we use **comparison and jump instructions** to achieve the same result. These instructions compare two values and then **jump** to a different part of the program based on the result of the comparison.

----

### **CMP Operation**

The `cmp` instruction is used to perform **comparison** operations. It compares the values of two operands and sets the **status flags** in the **EFLAGS register** based on the result of the comparison.

```
section .text
    .global _start

_start:
    mov eax, 5      ; Load value 5 into eax
    cmp eax, 10     ; Compare eax with 10
```

{: .important-title }
In this example, I compare the value in `eax` with `10`. The `cmp` instruction **subtracts** the second operand `10` from the first operand `5` but **does not store the result**. Instead, it sets the **status flags** in the **EFLAGS register** based on the result of the comparison which is `5 - 10 = -5`.

----

### **JMP Operation**

The `jmp` instruction is used to perform **unconditional jumps**. It transfers control to a different part of the program based on the specified label or memory address.

```
section .text
    .global _start

_start:
    mov eax, 5      ; Load value 5 into eax
    cmp eax, 10     ; Compare eax with 10
    jne not_equal   ; Jump to 'not_equal' if not equal
    jmp equal       ; Jump to 'equal' if equal

not_equal:
    mov ebx, 10     ; Load value 10 into ebx
    jmp end

equal:
    mov ebx, 5      ; Load value 5 into ebx

end:
    int 80h         ; End of the program
```

{: .important-title }
In this example, I compare the value in `eax` with `10`. If the values are **not equal**, I jump to the `not_equal` label. If the values are **equal**, I jump to the `equal` label. Finally, I reach the `end` label, which signifies the end of the program.

----

### **Conditional Jumps Table**

Here is a table of common conditional jumps in assembly language:

| Instruction | Description | Condition |
|:------------|:------------|:----------|
| `je`        | Jump if Equal | `ZF = 1` |
| `jne`       | Jump if Not Equal | `ZF = 0` |
| `jg`        | Jump if Greater | `ZF = 0 and SF = OF` |
| `jge`       | Jump if Greater or Equal | `SF = OF` |
| `jl`        | Jump if Less | `SF ≠ OF` |
| `jle`       | Jump if Less or Equal | `ZF = 1 or SF ≠ OF` |
| `ja`        | Jump if Above | `CF = 0 and ZF = 0` |
| `jae`       | Jump if Above or Equal | `CF = 0` |
| `jb`        | Jump if Below | `CF = 1` |
| `jbe`       | Jump if Below or Equal | `CF = 1 or ZF = 1` |

`SF = Sign Flag, OF = Overflow Flag, ZF = Zero Flag, CF = Carry Flag`