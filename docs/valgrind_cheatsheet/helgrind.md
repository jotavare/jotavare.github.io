---
title: Helgrind
nav_order: 4
layout: default
parent: 📑 Valgrind Cheatsheet
---

## **HELGRIND TIPS**

- Adhere to `pthread` best practices to minimize error occurrences.
- When crafting your `thread` functions or `alloc` functions that recycle a buffer pool, label them using macros from `helgrind.h`.

## **HELGRIND**

<div class="code-example" markdown="1">
Detect common threading errors in ./program.
</div>
```shell
valgrind --tool=helgrind --free-is-write=yes ./program
```

<div class="code-example" markdown="1">
Also detect potential deadlocks. Can be verbose for many programs.
</div>
```shell
valgrind --tool=helgrind --track-lockorders=yes ./program
```

## **HELGRIND ERRORS**

<div class="code-example" markdown="1">
Lock was unlocked without first being locked.
<br>Helgrind shows where it originated.
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
<br>Helgrind shows the backtrace for both threads’ accesses.
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