---
title: Procedures Basics
nav_order: 2
layout: default
parent: Procedures/Functions
grand_parent: 🔲 x86 Assembly NASM
---

## **PROCEDURES BASICS**

### **Defining Procedures**

A **procedure** in x86 assembly serves the same purpose as a **function** in higher-level languages. It encapsulates a **sequence of instructions** to perform a specific task.

In this example I define a procedure named `add_two`. The procedure adds the values stored in the `eax` and `ebx` registers and returns the result.

```
add_two:
    ADD eax, ebx  ; Add the contents of eax and ebx
    RET           ; Return from the procedure
```

----

### **Calling Procedures**

To call a procedure, we use the `call` instruction followed by the **name of the procedure**. After the procedure execution, control returns to the instruction immediately following the `call`.

```
    MOV eax, 2      ; Set eax to 2
    MOV ebx, 3      ; Set ebx to 3
    CALL add_two    ; Call the add_two procedure
```

{: .important-title }
When a procedure is called, the **return address is pushed onto the stack**. The `RET` instruction retrieves this return address from the stack, effectively returning control to the caller.

----

### **Debugging and Stack Inspection**

If I use GDB, I can inspect the stack to understand how return addresses are managed. 

```bash
info register ESP   ; Get the current value of ESP
x/x [esp]           ; Inspect the value at ESP
```

- The stack pointer `esp` points to the top of the stack, where the return address is stored.

{: .important-title }
Understanding how return addresses are stored on the stack is crucial for computer security. Exploits such as buffer overflows can manipulate return addresses to execute malicious code.

----

### **End Code**

```
section .data

section .text

global main

addTwo:             ; define a function called addTwo
    add eax, ebx    ; add the two arguments
    ret             ; return the result

main:
    mov eax, 4  ; set the first argument to 4
    mov ebx, 1  ; set the second argument to 1
    call addTwo ; call the addTwo function
    mov ebx,eax ; store the result of eax in ebx
    mov eax, 1  ; set eax to 1
    int 80h     ; exit the program
```

{: .important-title }
If write on bash `echo $?` after running the program, it will print the return value of the program. In this case, it will print `5`. Which is the result of `4 + 1 = 5`.