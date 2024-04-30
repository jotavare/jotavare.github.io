---
title: Memcheck
nav_order: 3
layout: default
parent: 📑 Valgrind Cheatsheet
---

## **MEMCHECK TIPS**

- Execute until the program terminates. Memcheck identifies numerous leaks upon conclusion.
- Prioritize testing an optimized version initially. An unoptimized version exhibits distinct errors.
- Employ personalized memory handling? Import `valgrind/valgrind.h` and resort to standard `malloc` and `free` if `RUNNING_ON_VALGRIND` macro evaluates to true.
- Opt for customized `alloc` functions? Notify valgrind of their usage via `VALGRIND_MALLOCLIKE_BLOCK` + `VALGRIND_FREELIKE_BLOCK`.

## **MEMCHECK**

Valgrind provides a suite of debugging tools to increase performance and fix problems with your programs. Memcheck is one of the more commonly used tools. This tool helps find memory-related errors that might cause your program to crash or leak memory.

Make sure you compile your program with `-g` to generate debugging symbols. Both GDB and Valgrind use these symbols to show line numbers in error messages. For more on compilation, see the [gcc wiki](https://bytes.usc.edu/cs104/wiki/gcc.md).

<div class="code-example" markdown="1">
Compile with debugging symbols.
</div>
```shell
g++ -Wall -std=c++11 -g program.cpp -o program
```

{: .important-title }
The MemCheck tool in Valgrind runs by default, so you don’t have to specify `--tool=memcheck` when running Valgrind. However, you can use the option to be explicit.

<div class="code-example" markdown="1">
Detect common memory errors in ./program.
</div>
```shell
valgrind ./program args
valgrind --tool=memcheck ./program args
```

<div class="code-example" markdown="1">
Detect memory errors and memory leaks.
</div>
```shell
valgrind --leak-check=yes ./program
```

<div class="code-example" markdown="1">
Run with more verbose for helpful error messages.
</div>
```shell
valgrind --tool=memcheck --leak-check=full ./program
```

<div class="code-example" markdown="1">
Take longer and trace the origin of uninitialized values.
</div>
```shell
valgrind --leak-check=yes --track-origins=yes ./program
```

<div class="code-example" markdown="1">
Detect unclosed file descriptors.
</div>
```shell
valgrind --track-fds=yes ./program
```

<div class="code-example" markdown="1">
Produce a `xtmemory.kcg` file.
<br>Install `KCachegrind` to examine it.
<br>It shows a visual backtrace of places in the code that leaked memory.
</div>
```shell
valgrind --xtree-memory=full --leak-check=yes ./program
```

<div class="code-example" markdown="1">
Run silently.
<br>Return a failure exit code if errors are found, rather than `./program` exit code.
<br>Useful in automated tests.
</div>
```shell
valgrind --error-exitcode=1 ./program
```

## **MEMCHECK ERRORS**

<div class="code-example" markdown="1">
Use of an uninitialized variable.
<br>Memcheck prints the backtrace where the value was used.
<br>`--track-origins=yes` can find where it came from.
</div>
```shell
Conditional jump or move depends on the uninitialized value(s)
    at 0x402DFA94: _IO_vfprintf (_itoa.h:49)
    by 0x402E8476: _IO_printf (printf.c:36)
    by 0x8048472: main (tests/manuel1.c:8)
```

<div class="code-example" markdown="1">
Read from memory that is not allocated.
<br>In this case in unused stack memory below the stack.
<br>Often `Memcheck` can say `“in freed memory”` etc.
</div>
```shell
Invalid read of size 4
    at 0x40F6BBCC: (within /usr/lib/libpng.so.2.1.0.9)
    ...
Address 0xBFFFF0E0 is not stack'd, malloc'd or free'd
```

{: .important-title }
Other common errors detected are `invalid pointers` in system calls, `double frees`, mixing `new/free`, overlapping `memcpy` and `realloc(0)`.