---
title: Breakpoints and Watchpoints
nav_order: 5
layout: default
parent: 📑 GDB Cheatsheet
---

## **BREAKPOINTS AND WATCHPOINTS**

| Command                                                  | Result                                                       |
| :------------------------------------------------------- | :----------------------------------------------------------- |
| `break [line/function]`                                  | Set a breakpoint on a line or function.                      |
| `break main.c:42`                                        | Set breakpoint at the file and (line or function).           |
| `tbreak [line/function]`                                 | Set a temporary breakpoint.                                  |
| `watch [variable]`                                       | Set a software watchpoint on a variable.                     |
| `info breakpoints`                                       | Show breakpoints and watchpoints.                            |
| `info watchpoints`                                       | Show current watchpoints.                                    |
| `delete [breakpoint/watchpoint number]`                  | Delete a breakpoint or watchpoint by number.                 |
| `delete`                                                 | Delete all breakpoints and watchpoints (prompted).           |
| `clear`                                                  | Delete breakpoints and watchpoints at the current line.      |
| `clear [line/function]`                                  | Delete breakpoints or watchpoints at a line or function.     |
| `disable [breakpoint/watchpoint number]`                 | Turn a breakpoint or watchpoint off, but don't remove it.    |
| `enable [breakpoint/watchpoint number]`                  | Turn a disabled breakpoint or watchpoint back on.            |
| `commands [breakpoint/watchpoint number] [commands] end` | Set GDB commands with a breakpoint or watchpoint.            |
| `ignore [breakpoint/watchpoint number] [n times]`        | Ignore a breakpoint or watchpoint n times before activation. |
| `condition [breakpoint/watchpoint number] [expression]`  | End only if the expression is true.                          |
| `condition [breakpoint/watchpoint number] [condition]`   | End only if the condition is true.                           |
| `condition [breakpoint/watchpoint number]`               | Delete condition at a breakpoint or watchpoint number.       |