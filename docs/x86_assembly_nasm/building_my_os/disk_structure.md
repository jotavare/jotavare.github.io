---
title: Disk Structure
nav_order: 3
layout: default
parent: Building My OS
grand_parent: 🔲 x86 Assembly NASM
---

## **DISK STRUCTURE**

<div style="text-align:center;">
    <br>
    <img src="../../../assets/images/disk_structure.jpg" alt="Disk Structure Diagram">
</div>

   - Disks consist of **stacked platters**;
   - Each platter with **two heads** (top and bottom) for **reading** and **writing** data;
   - Platters are divided into **tracks**, which are further divided into **sectors**;
   - Sectors typically have a standard size, often **512 bytes**, determined by the file format;
   - Tracks stacked across multiple disks form a **cylinder**;

----

### **Addressing Schemes**

Disk data is accessed using two primary addressing schemes:

**Cylinder-Head-Sector (CHS):**

- Historically used and still relevant for certain **legacy systems**;
- Specifies the **cylinder, head, and sector** of data;
- Aids in locating data on a physical disk;
- Useful for **partitioning** and older devices like floppy disks;

**Logical Block Addressing (LBA):**

- Utilizes a **linear addressing scheme** for modern disks, including **SSDs** and **network drives**;
- Blocks are **indexed numerically**, starting from zero;
- Offers easier **abstraction** and **compatibility** across different disk types;

----

### **Converting CHS and LBA**

The following formulas can be used to convert between `CHS` and `LBA`:

**CHS to LBA:**

- `LBA = (C * TH * TS) + (H * TS) + (S - 1)`;
- `C` - Cylinder, `H` - Head, `S` - Sector, `TH` - Total Heads, `TS` - Total Sectors;

**LBA to CHS:**

- `T` = `(LBA / Sectors per Track)`;
- `S` = `(LBA % Sectors per Track) +1`;
- `H` = `(T % Number of Heads)`;
- `C` = `(T / Number of Heads)`;

----

### **Practical Application**

- Understanding both addressing schemes is crucial for interacting with disk data through **system calls** and **interrupts**;
- Converting between `CHS` and `LBA` enables **compatibility** and efficient data access across different systems and storage devices;