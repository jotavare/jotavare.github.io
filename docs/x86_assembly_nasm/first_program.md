---
title: First Program
nav_order: 4
layout: default
parent: 🔲 x86 Assembly NASM
---

### **Why NASM?**

NASM offers a simplified syntax compared to the more complex AT&T syntax commonly used on Linux systems. It's designed to be **more approachable for beginners** while still providing all the necessary skills for x86 programming. Plus, **NASM is an assembler widely used in the industry**, making it a valuable tool to learn.

----

### **Setting up NASM**

Install NASM on your Linux system, as it's the most compatible environment for assembly programming.

```bash
sudo apt update
sudo apt -y install nasm
```

{:.important-title}
`-y` flag **automatically** confirms installation prompts.

Create a new file with a `.s`, `.as`, or `.asm` extension, such as `first.s`.

----

### **Program Structure**
- Divide your program into sections:
  - `section .data` stores variables used in the program.
  - `section .text` contains the actual code of the program.

```c
section .data

section .text
```

----

### **Starting Execution**
- Use the `global _start` directive to declare the entry point of your program.
- Define a label `_start:` to mark the beginning of the program execution.

```c
global _start

_start:
```

----

### **Writing Code**
- Use the `mov` instruction to move data between locations, such as registers.
- Example: `mov eax, 1` moves the value `1` into the `eax` register.
- You can move static values into registers for manipulation.
- `move destination, source`

```c
mov eax, 1
```

----

### **Ending the Program**
- To terminate the program, use an interrupt instruction `int`.
- Specify the desired action in the `eax` register.
- For example, `mov eax, 1` indicates the exit system call.
- Set the exit status code in the `ebx` register.
- Execute the interrupt with `int 0x80` (hexadecimal value `80`).

```c
mov eax, 1
mov ebx, 0
int 0x80
```

----

### **End Result**

```c
section .data

section .text
    global _start

_start:
    mov eax, 1
    mov ebx, 0
    int 0x80
```

----

### **Compiling with NASM**

<div class="code-example" markdown="1">
Use NASM to compile the assembly code into an object file `.o`.
</div>
```bash
nasm -f elf -o first.o first.s
```

----

### **Linking and Generating Executable**

<div class="code-example" markdown="1">
Link the object file to create an executable.
</div>
```bash
ld -m elf_i386 -o first first.o
```

{:.important-title}
`-m elf_i386` flag specifies the target architecture. **32 bits** for **x86**.

----

### **Running the Program**

<div class="code-example" markdown="1">
Execute the program using and verify the exit status code.
</div>
```bash
./first
echo $?
```

----

### **Debugging with GDB**

- Use **GDB (GNU Debugger)** for debugging assembly programs. Also works with C and C++.
- Set breakpoints and step through the program to observe execution.

<div class="code-example" markdown="1">
Start GDB and load the executable.
</div>
```bash
gdb first
```

----

### **GDB Commands**

| Command | Description |
|:--------|:------------|
| `layout asm` | Switch to assembly view. |
| `break _start` | Set a breakpoint at the start label. |
| `run` | Start program execution. |
| `stepi` | Step through one assembly instruction at a time. |
| `info registers` | View register values. |

{:.important-title}
You can check my GDB cheatsheet [here](https://jotavare.github.io/gdb_cheatsheet).