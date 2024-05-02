---
title: Two's Complement
nav_order: 4
layout: default
parent: Binary Basics
grand_parent: 🔲 x86 Assembly NASM
---

## **TWO'S COMPLEMENT**

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