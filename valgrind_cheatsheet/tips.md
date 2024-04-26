---
title: Tips
nav_order: 2
layout: default
parent: Valgrind Cheatsheet
---

- Output has no line numbers? Have build system compile with `-g`.
- Programs run 10-50x slower. Test with small workloads.
- Too many errors? Fix the first errors, that may remove further errors.
- Check out the `--vgdb-error` and `--vgdb-stop-at` options for using GDB to step through the program.