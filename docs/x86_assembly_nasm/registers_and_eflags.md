---
title: Registers and EFLAGS
nav_order: 4
layout: default
parent: 🔲 x86 Assembly NASM
---

## **REGISTERS AND EFLAGS**

### **Register Types**

| Register     | Description |
|:-------------|:------------|
| `EAX`        | Accumulator, used for multiplication and division. |
| `EBX`, `EDX` | General-purpose registers. |
| `ESI`, `EDI` | High-speed memory transfer registers. |
| `ECX`        | Loop counter register. |
| `ESP`        | Stack pointer, points to the next available location in stack memory. |
| `EBP`        | Base pointer, used to reference function parameters and local variables on the stack. |

----

### **Special Registers**

| Register | Description |
|:---------|:------------|
| `EIP`    | Instruction pointer, points to the address of the next instruction to execute. |
| `EFLAGS` | Flags register indicating the status of an operation. |

{: .important-title }
You can check more information about register types [here](https://en.wikibooks.org/wiki/X86_Assembly/X86_Architecture).

----

### **Register Size**

| Register   | Size    |
|:-----------|:--------|
| `EAX`      | 32 bits |
| `AX`       | 16 bits |  
| `AH`, `AL` | 8 bits  |

- **x86 Registers**, each register is **32 bits** in size.
- Registers like `EAX`, `EBX`, `ECX`, and `EDX` are standard, with the `E` denoting **extended access to all 32 bits**.
- Dropping the `E` to access only **16 bits** (e.g., `AX`, `BX`, `CX`, `DX`).
- Can also access **8-bit high** and **8-bit low** bytes (e.g., `AH`, `BH`, `CH`, `DH` and `AL`, `BL`, `CL`, `DL`).

----

### **EFLAGS**

This is a **32-bit register** in **x86 assembly** language that contains various flags providing information about the result of an operation. These flags are crucial for understanding the outcome of **arithmetic operations** and determining the **next steps in the program flow**.

| Flags | Description |
|:------|:------------|
| `CF`  | Carry flag, set when an arithmetic operation generates a carry or borrow. |
| `OF`  | Overflow flag, set when an operation generates a result too large for the destination register. |
| `SF`  | Sign flag, set when the result of an operation is negative. |
| `ZF`  | Zero flag, set when the result of an operation is zero. |
| `AC`  | Alignment check flag, set when an unaligned memory access occurs. |
| `PF`  | Parity flag, set when the least-significant byte of the result has an even number of set bits. |
| `IF`  | Interrupt flag, determines whether the CPU recognizes external interrupts. |

{: .important-title }
If the flag is set to `1`, it means the condition is met; otherwise, it's `0`. You can check more register flags [here](https://en.wikipedia.org/wiki/FLAGS_register).