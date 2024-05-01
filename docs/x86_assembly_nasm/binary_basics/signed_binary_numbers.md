---
title: Signed Binary Numbers
nav_order: 3
layout: default
parent: Binary Basics
grand_parent: 🔲 x86 Assembly NASM
---

### **Signed Binary Numbers**

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
The result `-4` is unexpected based on the law of arithmetic `A + (−A) = 0`. To properly represent negative numbers in binary, we utilize **two's complement**. In addition to the MSB sign bit for assigning a negative value, we apply the two's complement to negative numbers to obtain the correct result. This ensures accurate representation of negative values in binary arithmetic.