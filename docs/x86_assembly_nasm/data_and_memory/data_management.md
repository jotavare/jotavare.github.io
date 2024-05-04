---
title: Data Management
nav_order: 3
layout: default
parent: Data and Memory
grand_parent: 🔲 x86 Assembly NASM
---

## **DATA MANAGEMENT**

### **Data Section Declaration**
Declare variables and allocate memory in the data section. The **data section** is used to define **variables** and **constants**, specifying their **data type** and **initial values**.

```c
section .data
    variable_name data_type initial_value
    num dd 10
```

- **Variable Name** - Provide a name for the data variable.
- **Data Type** - Specify the size of the data, determining the number of bytes allocated.
- **Initial Value** - Assign an initial value to the variable.

----

### **Data Types and Sizes**

In assembly language, data is represented in binary form. There's **no inherent distinction between data types** like integers, characters, or strings. Instead, data is distinguished by its **memory allocation size**.

The data types commonly used in assembly language include:

| Data Type   | Description | Size (Bytes) | Size (Bits) |
| :---------- | :---------- | :----------- | :---------- |
| `DB`        | Byte        | 1            | 8           |
| `DW`        | Word        | 2            | 16          |
| `DD`        | Double Word | 4            | 32          |
| `DQ`        | Quad Word   | 8            | 64          |
| `DT`        | Ten Bytes   | 10           | 80          |

----

### **Accessing Data Addresses**

When referencing data variables, it's essential to understand that the **variable name** represents the **address of the data** rather than the **actual value**. Attempting to load the value of a variable `num` directly into a register like `ebx` will load its address, not its value.

```c
.section data
    num DD 5

section .text
    global _start

_start:
    MOV eax,1
    MOV ebx,[num] ; if i used num directly, it would be the address and not the value
    INT 80h
```

- When using `num`, the destination register would contain something akin to `$0x08048000`, representing the memory address where the variable `num` is stored.
- On the other hand, when using `[num]`, the destination register would hold `0x08048000` (without the $ sign), denoting the value stored in the variable `num`, which in this case is `5`.

{: .important-title }
In GDB, you can inspect registers with `info registers [register_name]` and analyze memory content with commands like `x/x [address]`.
