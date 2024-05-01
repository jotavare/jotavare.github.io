---
title: Binary Basics
nav_order: 2
layout: default
parent: 🔲 x86 Assembly NASM
has_children: true
---

## **BINARY NUMBERS**

### **Base 10 Number System**

Each digit's position in a number represents an integer value ranging from **0** to **9**.

Let's break down the **base 10** number `13`:

| 10^1 | 10^0 |
|:-----|:-----|
|  1   |  3   |

- The leftmost digit represents **10^1**, which equals **10**.
- The rightmost digit represents **10^0**, which equals **1**.

<div class="code-example" markdown="1">
When we sum up these values:
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
When we sum up these values:
</div>
```
> 2^3 + 2^2 + 2^1 + 2^0
> (1x2^3) + (0x2^2) + (1x2^1) + (0x2^0)
> 8 + 0 + 2 + 0 = 10
> 1010 = 10
```

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

- We have the binary number `100101` when read from **bottom** to **top**, and then from **left** to **right**.

<div class="code-example" markdown="1">
When we sum up these values:
</div>
```
> (1x2^0) + (0x2^1) + (1x2^2) + (0x2^3) + (0x2^4) + (1x2^5)
> 1 + 0 + 4 + 0 + 0 + 32 = 37
```

----

### **Byte and Bit Relationship**

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

----

### **Two's Complement**
The two's complement is a method used in computing to **represent both positive and negative integers** using binary numbers. It's particularly efficient for arithmetic operations because it simplifies addition and subtraction by treating positive and negative numbers uniformly.

To find the **two's complement** of a number:

1. **Invert (flip) all the bits**, changing **1s** to **0s** and **0s** to **1s**.
2. After inverting the bits, **add 1** to the result.

<div class="code-example" markdown="1">
Let's find the **two's complement** of the binary number `0000 0010`:
</div>
```
> 0000 0010 (Represents 2)
> 1111 1101 (Inverted all bits) (One's Complement)
> 1111 1110 (Added 1) (Two's Complement)
```

<div class="code-example" markdown="1">
The two's complement ensures that the **sum of a number and its negative counterpart equals zero**:
</div>
```
    1111 1110 (Two's Complement)
+   0000 0010 (represents 2)
-------------
(1) 0000 0000 (result is 0)
```

- The overflow, represented by (1), is handled by a **special register** called the `carry register`, which is not directly visible in the result.
- With this method, we satisfy the law of arithmetic `A + (−A) = 0`.

The **two's complement** representation has **several advantages**:
- It allows for the **representation of both positive and negative numbers** using the same binary system.
- It **simplifies arithmetic operations** like addition and subtraction because negative numbers are represented in a way that aligns well with addition.
- It **eliminates the need for a separate sign bit**, making the representation more compact and efficient for computation in computer hardware.

----

### **Hexadecimal Numbers**

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