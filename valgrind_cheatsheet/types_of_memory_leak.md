---
title: Types of Memory Leak
nav_order: 5
layout: default
parent: Valgrind Cheatsheet
---

## **TYPES OF MEMORY LEAK**

You will see two summaries at the end of Valgrind’s output: the heap summary and the leak summary. The heap summary tells you how many memory allocations occurred (how many times new was called directory or indirectly in your program) and how many bytes of memory were lost. Here’s some example output:

```bash
==29== HEAP SUMMARY:
==29==     in use at exit: 74,043 bytes in 11 blocks
==29==   total heap usage: 13 allocs, 2 frees, 74,115 bytes allocated
==29==
==29== LEAK SUMMARY:
==29==    definitely lost: 16 bytes in 2 blocks
==29==    indirectly lost: 0 bytes in 0 blocks
==29==      possibly lost: 0 bytes in 0 blocks
==29==    still reachable: 0 bytes in 0 blocks
==29==         suppressed: 74,027 bytes in 9 blocks
```

For an example of this, read through the errors above. Here is what the two most important parts of the summary mean:
- `definitely lost`: your program is leaking memory and you need to fix it!
- `indirectly lost`: your program may have crashed and couldn’t clean up memory.
- `suppressed`: you can safely ignore this area since this memory was not managed by your program.
- `possibly lost`: your program is leaking memory unless you’re doing odd things with pointers.

{: .important-title }
Suppressed memory is a memory still allocated when Valgrind exits that we tell Valgrind to ignore via a configuration file in your virtual machine. This memory is usually used by either the system’s dynamic library loader or parts of the standard library that use custom allocators and deallocators.

## **VALGRIND MANUAL DETAILED DESCRIPTION**

<div class="code-example" markdown="1">
A start-pointer or chain of start-pointers to the block is found. Since the block is still pointed at, the programmer could, at least in principle, have freed it before program exit. "Still reachable" blocks are very common and arguably not a problem. So, by default, Memcheck won't report such blocks individually.
</div>
```markdown
`Still reachable`
```

<div class="code-example" markdown="1">
This means that no pointer to the block can be found. The block is classified as "lost", because the programmer could not possibly have freed it at program exit, since no pointer to it exists. This is likely a symptom of having lost the pointer at some earlier point in the program. Such cases should be fixed by the programmer.
</div>
```markdown
`Definitely lost`
```

<div class="code-example" markdown="1">
This means that the block is lost, not because there are no pointers to it, but rather because all the blocks that point to it are themselves lost. For example, if you have a binary tree and the root node is lost, all its children nodes will be indirectly lost. Because the problem will disappear if the definitely lost block that caused the indirect leak is fixed, Memcheck won't report such blocks individually by default.
</div>
```markdown
`Indirectly lost`
```

<div class="code-example" markdown="1">
This means that a chain of one or more pointers to the block has been found, but at least one of the pointers is an interior-pointer. This could just be a random value in memory that happens to point into a block, and so you shouldn't consider this ok unless you know you have interior-pointers.
</div>
```markdown
`Possibly lost`
```