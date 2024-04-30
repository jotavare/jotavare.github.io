---
title: Processor Modes and Registers
nav_order: 3
layout: default
parent: 🔲 x86 Assembly NASM
---

## **PROCESSOR MODES**

### **Protected Mode**
- Protected mode is the native processor state for x86 devices.
- It's the primary mode for most programming tasks on x86 devices.
- Allows multiple processes to run concurrently.
- Each process has its own memory section and cannot directly access the memory of other processes.
- Prevents illegal operations that could lead to process failure or system instability.

### **Real Address Mode**
- Implemented in early Intel programming environments.
- Facilitates direct hardware access, useful for low-level hardware interactions.
- Typically, programmers remain in protected mode unless direct hardware access is required, then switch to real address mode temporarily.

### **System Management Mode**
- Provides an operating system environment for specific chip designs.
- Utilized for tasks like power management and security.
- Tailored for particular chip architectures, enabling chip-specific operating system functionalities.

----

## **REGISTERS**

### **Register Size**
- **x86 Registers**, each register is **32 bits** in size.
- Registers like `EAX`, `EBX`, `ECX`, and `EDX` are standard, with the `E` denoting **extended access to all 32 bits**.
- Dropping the `E` to access only **16 bits** (e.g., `AX`, `BX`, `CX`, `DX`).
- Can also access **8-bit high** and **8-bit low** bytes (e.g., `AH`, `BH`, `CH`, `DH` and `AL`, `BL`, `CL`, `DL`).

### **Register Types and Uses**

| Register | Description |
|:---------|:------------|
| `EAX`    | Accumulator, used for multiplication and division. |
| `EBX`, `EDX` | General-purpose registers. |
| `ESI`, `EDI` | High-speed memory transfer registers. |
| `ECX`    | Loop counter register. |
| `ESP`    | Stack pointer, points to the next available location in stack memory. |
| `EBP`    | Base pointer, used to reference function parameters and local variables on the stack. |

{: .important-title }
You can check more information about register types [here](https://en.wikibooks.org/wiki/X86_Assembly/X86_Architecture).

### **Special Purpose Registers**

| Register | Description |
|:---------|:------------|
| `EIP`    | Instruction pointer, points to the address of the next instruction to execute. |
| `EFLAGS` | Flags register indicating the status of an operation. |

| Flags | Description |
|:------|:------------|
| `CF`  | Carry flag, set when an arithmetic operation generates a carry or borrow. |
| `OF`  | Overflow flag, set when an operation generates a result too large for the destination register. |
| `SF`  | Sign flag, set when the result of an operation is negative. |
| `ZF`  | Zero flag, set when the result of an operation is zero. |
| `AC`  | Alignment check flag, set when an unaligned memory access occurs. |
| `PF`  | Parity flag, set when the number of set bits in the result is even. |

{: .important-title }
You can check more register flags [here](https://en.wikipedia.org/wiki/FLAGS_register).