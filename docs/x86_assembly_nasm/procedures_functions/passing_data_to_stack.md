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

The stack layout will look like this:
    
| Stack |
|:-----:|
| ret addr (sp) |
| 1 |
| 4 |

`sp = stack pointer`

{: .important-title }
If we call addTwo, how does it know that the first parameter is 4 and the second parameter is 1? Theres are various ways to pass parameters to a function. One of the most common ways is to push the parameters onto the stack in reverse order and create a base pointer to reference the parameters.

### Setting up a base pointer (EBP)

Before accessing the parameters, we need to set up a base pointer (EBP) to reference the stack frame.

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

The stack layout will look like this:

| Stack |
|:-----:|
| ebp (sp) |
| ret addr |
| 1 |
| 4 |

`sp = stack pointer`

{: .important-title }
The base pointer acts like the base of my stack frame. It helps me reference the parameters and local variables. If I had functions inside functions, I could use the base pointer to reference the parameters and local variables of the outer function and kinda seperate visually the stack frames by the base pointer. ebp is like the divider between the stack frames.

### Accessing Parameters and cleaning up the Stack

Parameters are accessed relative to the base pointer `ebp`.

```
addTwo:
    push ebp
    mov ebp, esp
    mov eax, [ebp + 8]  ; first parameter 1
    mov ebx, [ebp + 12] ; second parameter 4
    add eax, ebx
    pop ebp             ; restore the base pointer (delete the base pointer)
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
|:-----:|:-----:|
|       | ebp (sp) |
| +4    | ret addr |
| +8    | 1 |
| +12   | 4 |

`sp = stack pointer`

{: .important-title }
We can use x/x or x/4x to inspect the stack in GDB. This will help us understand how the stack is laid out and how we can access the parameters.

