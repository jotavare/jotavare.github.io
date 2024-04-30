---
title: Data and Stack Memory
nav_order: 5
layout: default
parent: 🔲 x86 Assembly NASM
---

## **DATA AND STACK MEMORY**

### **Data Section Declaration**
Declare variables and allocate memory in the data section of our program.

```c
section .data
    variable_name data_type initial_value
    num dd 10
```

1. **Variable Name**: Provide a name for the data variable.
2. **Data Type**: Specify the size of the data, determining the number of bytes allocated.
3. **Initial Value**: Assign an initial value to the variable.

### **Data Types and Sizes**

The data types commonly used in assembly language include:

| Data Type | Description | Size (Bytes) | Size (Bits) |
| --------- | ----------- | ------------ | ----------- |
| DB        | Byte        | 1            | 8           |
| DW        | Word        | 2            | 16          |
| DD        | Double Word | 4            | 32          |
| DQ        | Quad Word   | 8            | 64          |
| DT        | Ten Bytes   | 10           | 80          |

### **Understanding Binary Representation**

In assembly language, data is represented in binary form. There's no inherent distinction between data types like integers, characters, or strings. Instead, data is distinguished by its memory allocation size.

For example, declaring a variable as a double word (`dd`) allocates 32 bits (4 bytes) of memory space, with an initial value assigned.

## **Interacting with Data**

Once data is declared and initialized, we can interact with it using assembly instructions. Let's explore how to load data into registers and manipulate it.

### **Loading Data into Registers**

To load data into registers, we utilize instructions like `mov` (move). For instance, `mov eax, 1` moves the value 1 into the `eax` register.

### **Accessing Data Addresses**

When referencing data variables, it's essential to understand that the variable name represents the address of the data rather than the actual value.

For example, attempting to load the value of a variable `num` directly into a register like `ebx` will load its address, not its value.

### **Debugging and Troubleshooting**

When encountering issues with data manipulation, debugging tools like GDB (GNU Debugger) are invaluable.

- **Inspecting Registers**: Use `info registers` to examine register values.
- **Analyzing Memory**: Utilize commands like `x` to examine memory content.