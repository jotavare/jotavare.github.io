---
title: Passing Data to the Stack
nav_order: 3
layout: default
parent: Procedures/Functions
grand_parent: 🔲 x86 Assembly NASM
---

## **PASSING DATA TO THE STACK**

### **Stack Overview**

Let's take this simple code as an example:

```
addTwo:
    add eax, ebx
    ret

main:
    push 4
    push 1
    call addTwo
    mov ebx, eax
    mov eax, 1
    int 80h
```

The **stack layout** will look like this:
    
| Stack |
|:------|
| `ret` (return address) (sp) |
| `1` |
| `4` |

`sp = stack pointer`

{: .important-title }
If I call `addTwo`, how does it know that the first parameter is `4` and the second parameter is `1`!? One of the most common ways is to **create a base pointer** to reference the parameters.

----

### **Creating a Base Pointer**

Before accessing the parameters, I need to set up a **base pointer** `ebp` to **reference the stack frame**.

```
addTwo:
    push ebp
    mov ebp, esp
    add eax, ebx
    ret

main:
    push 4
    push 1
    call addTwo
    mov ebx, eax
    mov eax, 1
    int 80h
```

The **stack layout** will look like this:

| Stack |
|:------|
| `ebp` (sp) |
| `ret` (return address) |
| `1` |
| `4` |

`sp = stack pointer`

{: .important-title }
The `ebp` acts like the **base of my stack frame** and the **divider** between the stack frames. It helps me reference the parameters and local variables. If I had functions nested in functions, I could use the base pointer to reference the parameters and local variables of the outer function. 

----

### **Accessing and Cleaning the Stack**

Parameters are accessed relative to the base pointer `ebp`.

```
addTwo:
    push ebp
    mov ebp, esp
    mov eax, [ebp + 8]
    mov ebx, [ebp + 12]
    add eax, ebx
    pop ebp
    ret

main:
    push 4
    push 1
    call addTwo
    mov ebx, eax
    mov eax, 1
    int 80h
```

| Value | Stack |
|:------|:------|
|       | `ebp` (sp) |
| `+4`  | `ret` (return address) |
| `+8`  | `1` |
| `+12` | `4` |

`sp = stack pointer`

{: .important-title }
I can use `x/x` or `x/4x` to inspect the stack in **GDB**. This will help me understand how the stack is laid out and how I can access the parameters.