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

### **Decimal to Binary Conversion**

Let's convert 37 to Binary:

Division     | Result | Remainder
:------------|:-------|:---------
37/2         | 18     | 1 `(18*2 = 36 + 1 = 37)`
18/2         | 9      | 0
9/2          | 4      | 1
4/2          | 2      | 0
2/2          | 1      | 0
1/2          | 0      | 1

- Reading from bottom to top and then left to right = `100101`;

<div class="code-example" markdown="1">
When we sum up these values:
</div>
```shell
- (1x2^0) + (0x2^1) + (1x2^2) + (0x2^3) + (0x2^4) + (1x2^5)
- 1 + 0 + 4 + 0 + 0 + 32 = 37
```

### **Binary Representation in Computers**

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

### **Binary Addition**

- 0 + 0 = 0: When both bits are 0, the result is 0.
- 0 + 1 = 1: When one bit is 0 and the other is 1, the result is 1.
- 1 + 0 = 1: Similar to the previous case, the result is 1.
- 1 + 1 = 10: When both bits are 1, the result is 10 in binary, which equals 2 in decimal.

<div class="code-example" markdown="1">
Let's illustrate binary addition with an example:
</div>
```shell
    0110
+   0100
---------
    1010
```

Starting from the rightmost bits:

- Adding the bits in the 1's place: 0 + 0 = 0.
- Moving to the next bit: 1 + 0 = 1.
- Then: 1 + 1 = 10 (write down 0 and carry over 1).
- Finally: 0 + 0 (plus the carried over 1) = 1.

So, the result is `1010` in binary.

## Signed Binary Numbers

In signed binary numbers, the most significant bit (MSB) serves as the sign bit:

- 0: Represents a positive number.
- 1: Represents a negative number.

For example:

- 0000 0000: Represents the number 0.
- If the number is negative:
    - 1 000 0010: Represents -2.
    - 0 000 0010: Represents 2.
    - 1000 0100: Represents -4.

The relationship between a number and its negative counterpart is represented by the equation: `A+(−A)=0A+(−A)=0.`

### **Two's Complement**
The two's complement is a method used in computing to represent both positive and negative integers using binary numbers. It's particularly efficient for arithmetic operations because it simplifies addition and subtraction by treating positive and negative numbers uniformly.

To find the two's complement of a number:

1. Invert all bits: Start with the binary representation of the number you want to represent. To find its two's complement, invert (flip) all the bits, changing 1s to 0s and 0s to 1s.
2. Add 1: After inverting the bits, add 1 to the result.

For example, let's find the two's complement of the binary number 0000 0010:
- 0000 0010: Represents 2.
- Inverting all bits, we get 1111 1101 (one's complement).
- Adding 1, we get 1111 1110 (two's complement), which represents -2.

<div class="code-example" markdown="1">
The two's complement ensures that the sum of a number and its negative counterpart equals zero:
</div>
```yaml
   1111 1110 (represents -2)
+  0000 0010 (represents 2)
-----------
   1 0000 0000
```

This result represents 0 in signed binary numbers.

The two's complement representation has several advantages:
- It allows for the representation of both positive and negative numbers using the same binary system.
- It simplifies arithmetic operations like addition and subtraction because negative numbers are represented in a way that aligns well with addition.
- It eliminates the need for a separate sign bit, making the representation more compact and efficient for computation in computer hardware.

# Hexadecimal Numbers

Hexadecimal is a convenient way to represent binary numbers, especially in computing.

- It's a base 16 numbering system.
- It uses the digits 0-9 and the letters A-F to represent values from 10 to 15.

Example:
- 0 1 2 3 4 5 6 7 8 9 A B C D E F
- 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
- 0x10 in hexadecimal equals 16 in decimal.

<div class="code-example" markdown="1">
Converting binary to hexadecimal:
</div>
```yaml
0000 0000 -> 0x00
1111 1111 -> 0xFF

1111 -> F (15) = 1+2+4+8

0100 1101 -> 4D
```

So, 0100 1101 in binary equals 4D in hexadecimal.