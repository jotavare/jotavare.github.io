---
title: Memcheck
nav_order: 2
layout: default
parent: Valgrind Cheatsheet
---

# **MEMCHECK**

<div class="code-example" markdown="1">
Use Valgrind Memcheck to detect common memory errors in myprog.
</div>
```markdown
valgrind path/to/myprog myargs
```

<div class="code-example" bash="1">
Use Valgrind Memcheck to detect memory errors and memory leaks.
</div>
```bash
valgrind --leak-check=yes path/to/myprog
```

<div class="code-example" bash="1">
Take longer and trace the origin of uninitialized values.
</div>
```bash
valgrind --leak-check=yes --track-origins=yes myprog
```

<div class="code-example" bash="1">
Detect unclosed file descriptors.
</div>
```bash
valgrind --track-fds=yes myprog
```

<div class="code-example" bash="1">
Produce a xtmemory.kcg file. Install KCachegrind to examine it. It shows a visual backtrace of places in the code that leaked memory.
</div>
```bash
valgrind --xtree-memory=full --leak-check=yes myprog
```

<div class="code-example" bash="1">
Run silently. Return a failure exit code if errors found, rather than myprog’s exit code. Useful in automated tests.
</div>
```bash
valgrind --error-exitcode=1 myprog
```
