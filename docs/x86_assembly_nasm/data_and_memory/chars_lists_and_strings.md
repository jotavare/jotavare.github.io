---
title: Chars, Lists, and Strings
nav_order: 5
layout: default
parent: Data and Memory
grand_parent: 🔲 x86 Assembly NASM
---

## **CHARS, LISTS, AND STRINGS**

### **Character Data**

```
section .data
    char db 'A'  ; Define a single character 'A'

section .text
    global _start

_start:
    mov bl, [char]  ; Move the value of char to bl
    mov eax, 1      ; Move 1 to eax
    int 80h         ; Interrupt
```

{: .important-title }
If I run the code and print the exit code with `echo $?` in bash, I will see the **ASCII** value of `'A' (65)`. I can search for the **ASCII table** to verify this or use the `man ascii` command in the terminal.

----

### **List Data**

```
section .data
    list db 1, 2, 3, 4  ; Define a list of values with no null terminator
                        ; Each value is a byte in size

section .text
    global _start

_start:
    mov bl, [list]  ; Move the first value of list to bl
    mov eax, 1      ; Move 1 to eax
    int 80h         ; Interrupt
```

{: .important-title }
One thing I **omitted** in this code is the **null terminator**, something that I learned in `C`. In this case, I have a list of values, so I need to add the **null terminator** manually so I know when the list ends. I can use whatever value I want as long as it's not part of the list. For example, in this case, using `0` or `-1` would be a good choice `list db 1, 2, 3, 4, -1`.

----

### **String Data**

```
section .data
    string1 db 'ABA', 0  ; Define a string 'ABA' with null terminator
    string2 db 'CDE', 0  ; Define another string 'CDE' with null terminator

section .text
    global _start

_start:
    mov bl, [string1]  ; Move the first character of string1 to bl
    mov eax, 1         ; Move 1 to eax
    int 80h            ; Interrupt
```

{: .important-title }
In strings, it's a little bit easier to add the **null terminator** because I can just add it at the end of the string. The importance of adding a null terminator is to know when the string ends; otherwise, **I don't know where a slot of memory ends and another begins**.

----

### **GDB Tips**

By default, **GDB** uses **AT&T syntax** but to ensure consistency with **NASM** I can set **GDB** to use **Intel syntax**. This will make it easier to understand the code during debugging sessions.

<div class="code-example" markdown="1">
Command to set **Intel syntax** in **GDB**:
</div>
```bash
echo "set disassembly-flavor intel" > ~/.gdbinit
```

{: .important-title }
Also, in **GDB** I can use `x/x` to see the **memory address** in **hex** and `x/x2` to see the **next 2 memory addresses** and so on.