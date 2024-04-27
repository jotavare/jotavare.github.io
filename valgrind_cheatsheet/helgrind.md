---
title: Helgrind
nav_order: 4
layout: default
parent: Valgrind Cheatsheet
---

## **HELGRIND TIPS**

- Use `pthread` best practices or get many errors reported.
- If you write your thread functions, or `alloc` functions that reuse a pool of buffers, identify them with `helgrind.h` macros.

## **HELGRIND**

<div class="code-example" markdown="1">
Use Valgrind Helgrind to detect common threading errors in myprog.
</div>
```shell
valgrind --tool=helgrind --free-is-write=yes myprog
```

<div class="code-example" markdown="1">
Also detect potential deadlocks. Can be verbose for many programs.
</div>
```shell
valgrind --tool=helgrind --track-lockorders=yes prog
```

## **HELGRIND ERRORS**

<div class="code-example" markdown="1">
Lock was unlocked without first being locked.
Helgrind shows where it originated.
</div>
```shell
Thread #1 unlocked a not-locked lock at 0x7FEFFFA90
    at 0x4C2408D: pthread_mutex_unlock
    by 0x40073A: nearly_main (tc09_bad_unlock.c:27)
    by 0x40079B: main (tc09_bad_unlock.c:50)
   Lock at 0x7FEFFFA90 was first observed
    at 0x4C25D01: pthread_mutex_init
    by 0x40071F: nearly_main (tc09_bad_unlock.c:23)
    by 0x40079B: main (tc09_bad_unlock.c:50)
```

<div class="code-example" markdown="1">
Possible race.
Helgrind shows the backtrace for both threads’ accesses.
</div>
```shell
Thread #1 is the program's root thread

Thread #2 was created
...
Possible data race during read of size 4 at 0x601038 by thread #1
Locks held: none
    at 0x400606: main (simple_race.c:13)

This conflicts with a previous write of size 4 by thread #2
...
Location 0x601038 is 0 bytes inside global var "var" declared at simple_race.c:3
```

{: .important-title }
Helgrind also detects pthreads API misuses, as well as races and deadlocks.