---
title: Hexadecimal Numbers
nav_order: 5
layout: default
parent: Binary Basics
grand_parent: 🔲 x86 Assembly NASM
---

## **HEXADECIMAL NUMBERS**

Hexadecimal is a **convenient way to represent binary numbers**, especially in computing, due to its efficiency in both readability and compactness.

- It's a **base 16** numbering system.
- It uses the digits **0-9** and the letters **A-F** to represent values from **10 to 15**.

| Decimal | Hexadecimal |
|:--------|:------------|
| 0       | 0           |
| 1       | 1           |
| 2       | 2           |
| 3       | 3           |
| 4       | 4           |
| 5       | 5           |
| 6       | 6           |
| 7       | 7           |
| 8       | 8           |
| 9       | 9           |
| 10      | A           |
| 11      | B           |
| 12      | C           |
| 13      | D           |
| 14      | E           |
| 15      | F           |

- To understand better, we can divide the **binary number** into groups of **4 bits**.
- The reason for this is that every **4 bits represents a hexadecimal value**.

| Binary | 8 (2^3) | 4 (2^2) | 2 (2^1) | 1 (2^0) | Total   |
|:-------|:--------|:--------|:--------|:--------|:--------|
| 0000   |    0    |    0    |    0    |    0    |   0     |
| 1111   |    1    |    1    |    1    |    1    |  15 (F) |

<div class="code-example" markdown="1">
Let's convert **binary** to **hexadecimal** with the number `0100 1101`:
</div>
```
> 0100 = 0 + 0 + 4 + 0 = 4
> 1101 = 1 + 0 + 4 + 8 = 13 (D)

> 0100 1101 = 4D
```