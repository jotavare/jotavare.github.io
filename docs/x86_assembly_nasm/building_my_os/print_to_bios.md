---
title: Print to BIOS
nav_order: 3
layout: default
parent: Building My OS
grand_parent: 🔲 x86 Assembly NASM
---

## **PRINT TO BIOS**

### **First Steps**

Let's continue with the previous code and print a message to the screen using the bootloader, the program is set up as follows:

```
org 0x7c00
bits 16

main:
    mov ax, 0

    mov ds, ax
    mov es, ax
    mov ss, ax

    mov sp, 0x7c00
```

- `ax` is set to `0` to establish a consistent starting point for the program;
- `ds` (**data segment**), `es` (**extra segment**), and `ss` (**stack segment**) are initialized to `0` to clear them;
- `sp` is set to `0x7c00`, pointing to the bootloader address;

### **Print Function**

Before execution, registers `si`, `ax`, and `bx` are pushed onto the stack to preserve their values during the function's execution.

```
print:
    push si
    push ax
    push bx
```

- `si` (**source index**) used to store the address of the message string (**starting point**);
- `ax` utilized for passing parameters to **BIOS** interrupts; 
- These parameters include the function number `ah` and sometimes data to be printed `al`;
- `bx` is preserved by pushing it onto the stack but remains unused throughout the function;

### **Printing Loop**

Within the print function, a loop is established to iterate over the characters of the message string.

```
print_loop:
    lodsb
    or al, al
    jz print_done

    mov ah, 0x0e
    mov bh, 0
    int 0x10

    jmp print_loop
```

- `lodsb` loads a byte from the memory location specified by the `si` into the `al`;
- Additionally, it automatically increments the `si` register to point to the next byte in memory;
- `or al, al` checks if `al` is zero, indicating the end of the string;
- `jz print_done` if the zero flag is set, the program jumps to the `print_done` label;
- The character stored in `al` is printed to the screen using BIOS interrupt `0x10` with function `0x0e`;
- `jmp print_loop` jumps back to the `print_loop` label to continue iterating over the characters;

----

### **Running the Program**

```
org 0x7c00              ; set origin to 0x7c00, default address where the BIOS loads the bootloader

bits 16                 ; set the assembly to 16-bit mode, typical for bootloader code

main:
    mov ax, 0           ; clear the ax register
    mov ds, ax          ; set the data segment to 0, effectively clearing it
    mov es, ax          ; set the extra segment to 0, effectively clearing it
    mov ss, ax          ; set the stack segment to 0, effectively clearing it

    mov sp, 0x7c00      ; set the stack pointer to the bootloader address, where the bootloader is loaded
    mov si, os_boot_msg ; load the address of the OS boot message into the source index register
    call print          ; call the print function to print the OS boot message
    hlt                 ; Halt the processor, essentially doing nothing

halt:
    jmp halt            ; Infinite loop, jumping back to itself, effectively halting the processor indefinitely

print:
    push si             ; save the source index register on the stack
    push ax             ; save the ax register on the stack
    push bx             ; save the bx register on the stack

print_loop:
    lodsb               ; load the byte at the address in SI into AL and increment SI
    or al, al           ; check if AL is zero (end of string)
    jz print_done       ; if AL is zero, end of string, jump to print_done

    mov ah, 0x0e        ; set the BIOS teletype function to print the character in AL
    mov bh, 0           ; set the page number to 0
    int 0x10            ; call BIOS interrupt 0x10 to print the character in AL

    jmp print_loop      ; jump back to print_loop to continue printing characters

print_done:
    pop bx
    pop ax
    pop si
    ret

os_boot_msg:
    db "OS Booting...", 0x0D, 0x0A, 0

times 510-($-$$) db 0   ; fill the rest of the bootloader space with zeros to ensure it's padded up to 510 bytes
dw 0xaa55               ; boot signature, indicating to the BIOS that this is a bootable device
```