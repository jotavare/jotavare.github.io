---
title: Helgrind
nav_order: 4
layout: default
parent: Valgrind Cheatsheet
---

<div class="code-example" bash="1">
Use Valgrind Helgrind to detect common threading errors in myprog.
```bash
valgrind --tool=helgrind --free-is-write=yes myprog
```
</div>

<div class="code-example" bash="1">
Also detect potential deadlocks. Can be verbose for many programs.
</div>
```bash
valgrind --tool=helgrind --track-lockorders=yes prog
```
