---
title: Common Errors
nav_order: 7
layout: default
parent: 📑 Valgrind Cheatsheet
---

## **COMMON ERRORS**

Valgrind will tell you about possible errors in your program that may cause it to crash or have unexpected output. Here are a few examples of common errors:

### **X bytes in Y blocks are definitely lost**

This error is a memory leak that will show up in your Heap and Leak Summary. You have leaked memory and this error points you to where that memory was allocated.

Error example:

```bash
8 bytes in 1 blocks are definitely lost in loss record 1 of 7
   at 0x489C344: operator new[](unsigned long) (vg_replace_malloc.c:433)
   by 0x1091CB: main (valgrind-test.cpp:5)
```

Here is the code that caused this error. The line number points to the commented line where the lost memory was allocated.

```cpp
int ** matrix = new int*[2];
matrix[0] = new int[2];  // error points where memory was allocated
delete [] matrix;
```

### **Conditional jump or move depends on the uninitialized value(s)**

This error is caused if you forget to initialize variables before using or accessing them. You can usually re-run valgrind with the flag `--track-origins=yes` to see where the uninitialized value came from.

Error example:

```bash
Conditional jump or move depends on uninitialised value(s)
   at 0x1091D1: main (valgrind-test.cpp:9)
```

Example running with `--track-origins=yes` shows the line where you might want to make sure you’re initializing values or setting to `nullptr` where appropriate.

```bash
==5214== Conditional jump or move depends on uninitialised value(s)
==5214==    at 0x401968: ListTest::~ListTest() (listtest.cpp:20)
==5214==    by 0x401728: main (in /home/test)
==5214==  Uninitialised value was created by a heap allocation <=== PAY ATTENTION TO THESE NOTES
==5214==    at 0x4C2E89F: operator new[](unsigned long)
==5214==    by 0x4018EF: ListTest::ListTest() (listtest.cpp:8)
==5214==    by 0x40126D: main (in /home/test)
```

All the examples below would have caused this error:

```cpp
// Example 1
int j;
j += 6; // error

// Example 2
int s;
if (s == 66) { // error
  printf("Hello there, General Kenobi!");
}

// Example 3
int i;
while (i < 104) { // error
  printf("I'm still working on fixing Valgrind errors!\n");
}
```

### **Invalid read/write of size X**

This error happens if you delete memory and try to access it in some way. Valgrind will tell you where the read or write occurred as well as where the memory was originally allocated. Unfortunately, Valgrind doesn’t tell you where the delete occurred.

Error example:

```bash
Invalid read of size 8
   at 0x10922C: main (valgrind-test.cpp:17)

Block was alloc'd at
   by 0x1091D9: main (valgrind-test.cpp:7)

Invalid write of size 4
   at 0x10922F: main (valgrind-test.cpp:17)
Address 0x0 is not stack'd, malloc'd or (recently) free'd
```

This was caused by the following code:

```cpp
int * matrix = new int[2];
delete [] matrix;
matrix[1] = 2;
```

### **Mismatched free/delete**

```bash
==91== Mismatched free() / delete / delete []
==91==    at 0x4C3123B: operator delete(void*) 
==91==    by 0x109C94: StarWars::operator=(StarWars const&) (starwars.cpp:183)
==91==    by 0x10A6F1: StarWars::execute() (starwars.cpp:365)
==91==    by 0x10A577: StarWars::order66() (starwars.cpp:334)
==91==    by 0x10B9A2: main (test-your-faith.cpp:33)
```

This is caused by incorrectly deleting a pointer to an array. If you’re deleting a single object (i.e. `int *`), you can deallocate memory with `delete`.

However, if you’re deleting an array object (i.e. `int **`), you need to use `delete []`. This also applies to higher-level pointers (i.e. `int ***`, `int ****`).

Here’s an example:

```cpp
int * a = new int;
delete a;           // note delete [] a; would also work

int ** A = new int[10];
delete [] A;

// the code below, would cause a mismatched free/delete error
int ** B = new int[10];
delete B;
```