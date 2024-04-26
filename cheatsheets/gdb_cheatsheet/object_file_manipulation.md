---
title: Object File Manipulation
nav_order: 9
layout: default
parent: GDB Cheatsheet
grand_parent: Cheatsheets
---

# **OBJECT FILE MANIPULATION**

| Command                | Result                                |
| :--------------------- | :------------------------------------ |
| `file [object]`        | Load new file for debug (sym+exec).   |
| `file`                 | Discard sym+exec file info.           |
| `symbol-file [object]` | Load only symbol table.               |
| `exec-file [object]`   | Specify object to run (not sym-file). |
| `core-file [core]`     | Post-mortem debugging.                |