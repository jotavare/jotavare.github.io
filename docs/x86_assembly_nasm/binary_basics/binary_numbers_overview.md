---
title: Binary Numbers Overview
nav_order: 1
layout: default
parent: Binary Basics
grand_parent: 🔲 x86 Assembly NASM
---

## **BINARY NUMBERS OVERVIEW**

----

### **Base 10 Number System**

Each digit's position in a number represents an integer value ranging from **0** to **9**.

Let's break down the **base 10** number `13`:

| 10^1 | 10^0 |
|:-----|:-----|
|  1   |  3   |

- The leftmost digit represents **10^1**, which equals **10**.
- The rightmost digit represents **10^0**, which equals **1**.

<div class="code-example" markdown="1">
When I sum up these values:
</div>
```
> (1x10^1) + (3x10^0)
> (1x10) + (3x1)
> 10 + 3 = 13
```

----

### **Binary Number System**

- Binary numbers are represented using only two symbols: **0 (off)** and **1 (on)**.
- Each digit's position represents a **power of 2**.
- The rightmost digit represents **2^0**, the next one **^1,** then **2^2**, and so on.

So, let's break down the binary number `1010`:

| 2^3 | 2^2 | 2^1 | 2^0 |
|:----|:----|:----|:----|
|  1  |  0  |  1  |  0  |

- The leftmost digit represents **2^3**, which equals **8**.
- The next digit to the left represents **2^2**, which equals **4**.
- The next digit to the left represents **2^1**, which equals **2**.
- The rightmost digit represents **2^0**, which equals **1**.

<div class="code-example" markdown="1">
When I sum up these values:
</div>
```
> 2^3 + 2^2 + 2^1 + 2^0
> (1x2^3) + (0x2^2) + (1x2^1) + (0x2^0)
> 8 + 0 + 2 + 0 = 10
> 1010 = 10
```

----

### **Byte and Bit**

| Unit | Size |
|:-----|:-----|
| Byte | 1 |
| Bits | 8 |

- **1 byte** consists of **8 bits**.

----

### **Binary Positional Notation**

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|:----|:---|:---|:---|:-:|:-:|:-:|:-:| 
|  0  |  0 |  0 |  0 | 0 | 0 | 0 | 0 |

- Binary numbers are represented using **8 bits**.
- Each bit represents a specific value, ranging from **1** to **128**.

----

### **Binary Counting**

- Computers count in binary, starting from **0** to **255**.
- The value **255** is represented by setting all bits to **1** in a byte.