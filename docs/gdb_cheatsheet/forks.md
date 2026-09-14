---
title: Forks
nav_order: 16
layout: default
parent: 📑 GDB Cheatsheet
---

## **FORKS**

| Command                        | Result                                                                               |
| :----------------------------- | :----------------------------------------------------------------------------------- |
| `set follow-fork-mode parent`  | Keep debugging the parent after a fork; the child runs free. This is the default.    |
| `set follow-fork-mode child`   | Follow the child after a fork; the parent runs free.                                 |
| `show follow-fork-mode`        | Display the current debugger response to a fork or vfork call.                       |
| `set detach-on-fork.`          | Debug both the parent and child processes.                                           |
| `set detach-on-fork [on/off]`  | Detach one of the processes after a fork, or retain debugger control over them both. |
| `show detach-on-fork [on/off]` | Show whether detach-on-fork mode is on/off.                                          |
| `set follow-exec-mode [mode]`  | Set debugger response to a program call of exec.                                     |
| `[new]`                        | Creates a new inferior and rebinds the process to this new inferior.                 |
| `[same]`                       | Keeps the process bound to the same inferior.                                        |