---
title: Signed Binary Numbers
nav_order: 3
layout: default
parent: Binary Basics
grand_parent: 🔲 x86 Assembly NASM
---

## **SIGNED BINARY NUMBERS**

In signed binary numbers, the **most significant bit (MSB)** serves as the **sign bit**:

- `0` - Represents a **positive number**.
- `1` - Represents a **negative number**.

The relationship between a number and its negative counterpart is represented by the equation, which is a **law in arithmetic**, `A + (−A) = 0`.

<div class="code-example" markdown="1">
Let's do an example for **negative numbers**:
</div>
```
> 0 000 0000 = 0
> 1 000 0010 = -2
> 0 000 0010 = 2

  1 000 0010 (Represents -2)
+ 0 000 0010 (Represents 2)
------------
  1 000 0100 (Represents -4)
```

{: .important-title }
The unexpected result of `-4` contradicts the **arithmetic law** `A + (−A) = 0`. Alongside utilizing the **MSB sign bit** to denote negative values, I employ **two's complement** to accurately represent negative numbers in binary arithmetic.