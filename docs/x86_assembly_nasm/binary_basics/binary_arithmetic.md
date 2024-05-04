---
title: Binary Arithmetic
nav_order: 2
layout: default
parent: Binary Basics
grand_parent: 🔲 x86 Assembly NASM
---

## **BINARY ARITHMETIC**

----

### **Binary Addition**

- `0 + 0 = 0` - When **both bits are 0**, the result is **0**.
- `0 + 1 = 1` - When **one bit is 0** and the **other is 1**, the result is **1**.
- `1 + 0 = 1` - Similar to the previous case, the result is **1**.
- `1 + 1 = 10` - When **both bits are 1**, the result is **10** in binary, which **equals 2 in decimal**.

<div class="code-example" markdown="1">
Let's illustrate binary addition with an example:
</div>
```
    0110
+   0100
---------
    1010
```

Starting from the rightmost bits:

- Adding the bits in the 1's place: **0 + 0 = 0**.
- Moving to the next bit: **1 + 0 = 1**.
- Then: **1 + 1 = 10** (write down **0** and **carry over 1**).
- Finally: **0 + 0** (plus the **carried-over 1**) = **1**.

So, the result is `1010` in binary.

----

### **Decimal to Binary Conversion**

Let's convert `37` to Binary:

Division     | Result | Remainder
:------------|:-------|:---------
37/2         | 18     | 1 `(18*2 = 36) (36 + 1 = 37)`
18/2         | 9      | 0
9/2          | 4      | 1
4/2          | 2      | 0
2/2          | 1      | 0
1/2          | 0      | 1

- I have the binary number `100101` when read from **bottom** to **top**, and then from **left** to **right**.

<div class="code-example" markdown="1">
When I sum up these values:
</div>
```
> (1x2^0) + (0x2^1) + (1x2^2) + (0x2^3) + (0x2^4) + (1x2^5)
> 1 + 0 + 4 + 0 + 0 + 32 = 37
```