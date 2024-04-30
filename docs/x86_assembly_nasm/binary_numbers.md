---
title: Binary Numbers
nav_order: 2
layout: default
parent: 🔲 x86 Assembly NASM
---

## **BINARY NUMBERS**

### **Base 10 Number System**

Each digit's position in a number represents an integer value ranging from 0 to 9.

So, let's break down the base 10 number `13`:

| 10^1 | 10^0 |
|:-----|:-----|
|  1   |  3   |

- The leftmost digit represents 10^1, which equals 10.
- The rightmost digit represents 10^0, which equals 1.

<div class="code-example" markdown="1">
When we sum up these values:
</div>
```shell
- (1x10^1) + (3x10^0)
- (1x10) + (3x1)
- 10 + 3 = 13
```

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
```shell
> 2^3 + 2^2 + 2^1 + 2^0
> (1x2^3) + (0x2^2) + (1x2^1) + (0x2^0)
> 8 + 0 + 2 + 0 = 10
> 1010 = 10
```

## **Decimal to Binary Conversion**

Let's convert 37 to Binary:

Division     | Result | Remainder
:------------|:-------|:---------
37/2         | 18     | 1 `(18*2 = 36 + 1 = 37)`
18/2         | 9      | 0
9/2          | 4      | 1
4/2          | 2      | 0
2/2          | 1      | 0
1/2          | 0      | 1

- Reading from bottom to top and then left to right `100101`;

<div class="code-example" markdown="1">
When we sum up these values:
</div>
```shell
- (1x2^0) + (0x2^1) + (1x2^2) + (0x2^3) + (0x2^4) + (1x2^5)
- 1 + 0 + 4 + 0 + 0 + 32 = 37
```

## **Binary Representation in Computers**

### **Byte and Bit Relationship**
| Byte | 1 |
|:-----|:--|
| Bits | 8 |

- **1 byte** consists of **8 bits**.

### **Binary Positional Notation**
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|:----|:---|:---|:---|:-:|:-:|:-:|:-:| 
|  0  |  0 |  0 |  0 | 0 | 0 | 0 | 0 |

- Binary numbers are represented using **8 bits**.
- Each bit represents a specific value, ranging from **1** to **128**.

### **Binary Counting**

- Computers count in binary, starting from **0** to **255**.
- The value **255** is represented by setting all bits to **1** in a byte.

## **Binary Addition**
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 10

0110
0100
---- +
1010

## Signed Binary Numbers

- Most significant bit (MSB) is the sign bit
- 0 positive
- 1 negative

0000 0000 = 0

if number is negative

1 000 0010 = -2
0 000 0010 = 2
----------
1000 0100 = -4

0 positive
1 negative


A + (-A) = 0

## Two's Complement

- Invert all bits
- Add 1

0000 0010 = 2
1111 1101 = -2 (invert all bits) one's complement
---------
        1 (add 1)

   1111 1110 = -2 (two's complement)
   0000 0010
   ---------
1  0000 0000

# Hexadecimal Numbers

Just a better way to represent binary numbers

- Base 16
- 0-9 and A-F

Example:
- 0 1 2 3 4 5 6 7 8 9 A B C D E F
- 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
- 0x10 = 16

0000 0000
1111 1111

1111 -> F (15) = 1+2+4+8

0100 1101 = 4D
---------
4    D(13)