---
title: History Display
nav_order: 12
layout: default
parent: 📑 GDB Cheatsheet
---

## **HISTORY DISPLAY**

| Command                                   | Result                                                                      |
| :---------------------------------------- | :-------------------------------------------------------------------------- |
| `show commands`                           | Print command history.                                                      |
| `info editing`                            | Print command history.                                                      |
| `set history filename [fname]`            | Set the name of the GDB command history file to fname.                      |
| `set history save`                        | Record command history in a file.                                           |
| `set history save [on/off]`               | Record or don't record the command history into the file specified.         |
| `set history size [size]`                 | Set the number of commands gdb keeps in its history list based on the size. |
| `set history size unlimited`              | Set the number of commands gdb keeps in its history list as unlimited.      |
| `set history remove-duplicates [count]`   | Removed the first duplicate entry in history based on the count.            |
| `set history remove-duplicates unlimited` | Removed dupicate entrys in history.                                         |
| `set history expansion [on/off]`          | Enable or disable history expansion.                                        |
| `show history`                            | Display all four history states.                                            |
| `show history filename`                   | Display the history of filename.                                            |
| `show history save`                       | Display the history of save.                                                |
| `show history size`                       | Display the history of size.                                                |
| `show history exp`                        | Display the history of exp.                                                 |
| `show commands`                           | Display the last ten commands in the command history.                       |
| `show commands [n]`                       | Print ten commands centered on command number n.                            |
| `show commands +`                         | Print ten commands just after the commands last printed.                    | 
| `break class::[member]`                   | Set breakpoint on class member. May get a menu.                             |
| `list class::[member]`                    | List member in class.                                                       |
| `ptype [class]`                           | Print class members.                                                        |
| `print [*this]`                           | Print contents of this pointer.                                             |
| `rbreak [regular expression]`             | Useful for breakpoint on overloaded member name.                            |