---
title: Machine-Level Debug
nav_order: 11
layout: default
parent: 📑 GDB Cheatsheet
---

## **MACHINE-LEVEL DEBUG**

| Command                 | Result                                             |
| :---------------------- | :------------------------------------------------- |
| `info registers`        | Print registers sans floats.                       |
| `info all-registers`    | Print all registers.                               |
| `print/x [$pc]`         | Print one register.                                |
| `stepi`                 | Single step at machine level.                      |
| `nexti`                 | Single step (over functions) at the machine level. |
| `display/i [$pc]`       | Print current instruction in display.              |
| `x/x [&gx]`             | Print variable gx in hex.                          |
| `info line [42]`        | Print addresses for object code for line 42.       |
| `info line [*0x2c4e]`   | Print line number of object code at address.       |
| `x/10i [main]`          | Disassemble first 10 instructions in main.         |
| `disassemble [address]` | Dissassemble code for function around address.     |