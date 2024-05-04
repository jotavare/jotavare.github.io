---
title: x86 Processor Overview
nav_order: 1
layout: default
parent: x86 Processor Architecture
grand_parent: 🔲 x86 Assembly NASM
---

## **X86 Processor Overview**

### **Processor Components**

<div style="text-align:center;">
    <br>
    <img src="../../../assets/images/x86_processor_diagram.png" alt="x86 Processor Diagram">
</div>

Basic components of the x86 processor to other hardware elements within the system:

- **CPU**: The central processing unit, responsible for executing instructions.
- **Memory**: Stores data and instructions for the CPU to access.
- **I/O Devices**: Input/output devices such as monitors, keyboards, and mice.

----

### **Processor Modes**

In **x86 architecture** exists **three primary modes** of operation:

- **Protected Mode**:
  - Protected mode is the native processor state for x86 devices.
  - It's the primary mode for most programming tasks on x86 devices.
  - Allows multiple processes to run concurrently.
  - Each process has its memory section and cannot directly access the memory of other processes.
  - Prevents illegal operations that could lead to process failure or system instability.

- **Real Address Mode**:
  - Implemented in early Intel programming environments.
  - Facilitates direct hardware access, useful for low-level hardware interactions.
  - Typically, programmers remain in protected mode unless direct hardware access is required, then switch to real address mode temporarily.

- **System Management Mode**:
  - Provides an operating system environment for specific chip designs.
  - Utilized for tasks like power management and security.
  - Tailored for particular chip architectures, enabling chip-specific operating system functionalities.

----

### **Communication Channels**

Communication between these components occurs through three primary buses:

1. **Control Bus**: Synchronizes actions among attached devices, facilitating coordination.
2. **Address Bus**: Holds the address of instructions and data during transfers.
3. **Data Bus**: Transfers instructions and data between the CPU, memory, and I/O devices.