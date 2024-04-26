---
title: Signal Control
nav_order: 10
layout: default
parent: GDB Cheatsheet
---

# **SIGNAL CONTROL**

| Command                | Result                                      |
| :--------------------- | :------------------------------------------ |
| `info signals`         | Print signal setup.                         |
| `handle signo actions` | Set debugger actions for signal.            |
| `handle INT print`     | Print message when signal occurs.           |
| `handle INT noprint`   | Don't print message.                        |
| `handle INT stop`      | Stop program when signal occurs.            |
| `handle INT nostop`    | Don't stop program.                         |
| `handle INT pass`      | Allow the program to receive a signal.      |
| `handle INT nopass`    | Debugger catches signal; program doesn't.   |
| `signal signo`         | Continue and send signal to program.        |
| `signal 0`             | Continue and send no signal to the program. |