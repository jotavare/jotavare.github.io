---
title: Memcheck
nav_order: 1
layout: default
parent: Valgrind Cheatsheet
---

Use Valgrind Memcheck to detect common memory errors in myprog.
```valgrind path/to/myprog myargs```

Use Valgrind Memcheck to detect memory errors and memory leaks.
```valgrind --leak-check=yes path/to/myprog```

Take longer and trace the origin of uninitialized values.
```valgrind --leak-check=yes --track-origins=yes myprog```

Detect unclosed file descriptors.
```valgrind --track-fds=yes myprog```

Produce a xtmemory.kcg file. Install KCachegrind to examine it. It shows a visual backtrace of
places in the code that leaked memory.
```valgrind --xtree-memory=full --leak-check=yes myprog```

Run silently. Return a failure exit code if errors found, rather than myprog’s exit code. Useful in
automated tests.
```valgrind --error-exitcode=1 myprog```
