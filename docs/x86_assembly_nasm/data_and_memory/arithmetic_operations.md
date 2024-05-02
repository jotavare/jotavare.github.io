---
title: Arithmetic Operations
nav_order: 5
layout: default
parent: Data and Memory
grand_parent: 🔲 x86 Assembly NASM
---

## **ARITHMETIC OPERATIONS**

### **ADD Operation**

The `add` instruction is used to perform **addition** operations.

```
section .data

section .text
    global _start

_start:
    mov eax, 2      ; Load value 5 into eax
    mov ebx, 3      ; Load value 3 into ebx
    add eax, ebx    ; Add ebx to eax
```

{: .important-title }
This instruction adds the value in `ebx` to `eax` and stores the result in `eax`. So, after this operation, `eax` should contain the **sum of the two numbers** `5`. Also, we can use a number like `2` in **binary** as `0b00000010` and in **hexadecimal** as `0x02`.

----

### **Handling Carry Flag**

The **Carry Flag** `CF` is another crucial aspect, especially when dealing with arithmetic operations involving **limited register sizes**. Consider a scenario where the result **exceeds the capacity** of the destination **register**.

```
section .data

section .text
    global _start

_start:
    mov al, 0xFF    ; Load value 255 into al
    mov bl, 1       ; Load value 1 into bl
    add al, bl      ; Add 1 to al
```

{: .important-title }
In this case, the result of the addition operation is `256`, which is **too large** to fit into the `al` register. In such cases, the **extra bits are carried over** and stored in the `CF` of the **EFLAGS register**. We can utilize the `adc` instruction to incorporate this carry into subsequent operations.

----

### **ADC Operation**

The `adc` **(add with carry)** instruction is used to perform **addition** operations **with a carry**.

```
section .data

section .text
    global _start

_start:
    mov al, 0xFF    ; Load value 255 into al
    mov bl, 1       ; Load value 1 into bl
    add al, bl      ; Add 1 to al
    adc al, 0       ; Add the carry flag to the result
```

{: .important-title }
In this case, the `adc` instruction adds the value in the `CF` to the result of the previous addition operation. This allows us to handle scenarios where the result **exceeds the capacity** of the destination **register** and **carry over the extra bits**.

----

### **SUB Operation**

The `sub` instruction is used to perform **subtraction** operations.

```
section .data

section .text
    global _start

_start:
    mov al, 5       ; Load value 5 into al
    mov bl, 3       ; Load value 3 into bl
    sub al, bl      ; Subtract 3 from 5
```

{: .important-title }
This instruction subtracts the value in `bl` from `al` and stores the result in `al`. So, after this operation, `al` should contain the **difference of the two numbers** `2`.

Now, as an example, let's **flip the numbers** and see what happens:

```
section .data

section .text
    global _start

_start:
    mov al, 3       ; Load value 3 into al
    mov bl, 5       ; Load value 5 into bl
    sub al, bl      ; Subtract 5 from 3
```

{: .important-title }
In this case, the result of the subtraction operation is `-2`, which is a **negative number**. The `SF` **(Sign Flag)** in the **EFLAGS register** will be set to `1` to indicate that the result is **negative**.

Another example, what if we subtract a **negative number** with a **positive number** `-2 + 2`:

```
section .data

section .text
    global _start

_start:
    mov eax, 3      ; Load value 5 into eax
    mov ebx, 5      ; Load value 2 into ebx
    sub eax, ebx    ; Subtract 2 from 5
    mov ebx, 2      ; Load value 2 into ebx
    add eax, ebx    ; Add -2 to 2
```

{: .important-title }
In this case, the result of the subtraction operation is `0`, which is the **sum of the two numbers**. The `ZF` **(Zero Flag)** in the **EFLAGS register** will be set to `1` to indicate that the result is **zero**.

----

### **MUL Operation**

The `mul` instruction is used to perform **multiplication** operations, primarily for **unsigned integers**.

```
section .data

section .text
    global _start

_start:
    mov al, 2       ; Load value 5 into al
    mov bl, 3       ; Load value 3 into bl
    mul bl          ; Multiply al by bl
```

{: .important-title }
In this case, the `mul` instruction multiplies the value in `bl` by `al` and stores the result in `al`. So, after this operation, `al` should contain the **product of the two numbers** `6`. The `a` register is a special register called the **accumulator**, its used for multiplication as the default destination for the operation.

In multiplication it's interesting, because it only **requires one operand**, the other operand is implicitly the `al` register. The result of the multiplication operation is stored in the **pair of registers** `ax` and `dx`. The `ax` register contains the **lower 16 bits** of the result, while the `dx` register contains the **higher 16 bits**.

Let's see another example with `mul`, where we **multiply two unsigned numbers** but the result is **too large** to fit in the `ax` register:

```
section .data

section .text
    global _start

_start:
    mov al, 0xFF    ; Load value 255 into al
    mov bl, 2       ; Load value 2 into bl
    mul bl          ; Multiply al by bl
```

{: .important-title }
In this case, the result of the multiplication operation is `510`, which is **too large** to fit into the `al` register. The **extra bits** are stored in the `ax` register.

## **IMUL Operation**

The `imul` instruction is used to perform multiplication operations, primarily for **signed integers**.

Now, let's see an example with `imul` where we **multiply two unsigned numbers**:

```
section .data

section .text
    global _start

_start:
    mov al, 0xFF    ; Load value 255 (unsigned) into al = -1 (signed)
    mov bl, 2       ; Load value 2 (unsigned) into bl = 2 (signed)
    imul bl         ; Multiply al by bl
    int 80h         ; Interrupt
```

{: .important-title }
`al` in this case will be equal to `-2`. Even tho I used **unsigned numbers**, the program **assumes the values are signed** because of `imul`, so the result of the multiplication operation is `-2`, which is **correct**: `2 * -1 = -2`. 

----

## **DIV Operation**

The `div` instruction is used to perform **division** operations.

```
section .data

section .text
    global _start

_start:
    mov eax, 11      ; Load value 11 into eax
    mov ecx, 2       ; Load value 2 into ecx
    div ecx          ; Divide eax by ecx = 5 remainder 1
    int 80h          ; Interrupt
```

{: .important-title }
In this case, the `div` instruction divides the value in `eax` by `ecx` and stores the **quotient** in `eax` and the **remainder** in `edx`. So, after this operation, `eax` should contain the **quotient** `5` and `edx` should contain the **remainder** `1`. `edx` and not `ecx` because `div` uses `edx:eax` as the dividend.

----

## **IDIV Operation**

The `idiv` instruction is used to perform **division** operations, primarily for **signed integers**.

```
section .data

section .text
    global _start

_start:
    mov eax, 0xff    ; Load value 255 (unsigned) into eax = -1 (signed)
    mov ecx, 2       ; Load value 2 into ecx
    idiv ecx         ; Divide eax by ecx = -1 remainder 1
    int 80h          ; Interrupt
```

{: .important-title }
In this case, the `idiv` instruction divides the value in `eax` by `ecx` and stores the **quotient** in `eax` and the **remainder** in `edx`. So, after this operation, `eax` should contain the **quotient** `-1` and `edx` should contain the **remainder** `1`.


