---
title: Browsing Data
nav_order: 8
layout: default
parent: GDB Cheatsheet
grand_parent: Cheatsheets
---

# **BROWSING DATA**

| Command                               | Result                                        |
| :------------------------------------ | :-------------------------------------------- |
| `print [expression]`                  | Print variable, added to value history.       |
| `print/x [expression]`                | Print variable in hex format.                 |
| `print [array[i]@count]`              | Artificial array - print array range.         |
| `print $`                             | Print last value.                             |
| `print *$->next`                      | Print thru history list.                      |
| `print $1`                            | Print value 1 from value history.             |
| `print ::gx`                          | Force scope to be global.                     |
| `print [basic.c]::gx`                 | Global scope in named file.                   |
| `print/x [&main]`                     | Print address of function.                    |
| `x/countFormatSize [address]`         | Low-level examine command.                    |
| `x/x [&gx]`                           | Print gx in hex.                              |
| `x/4wx [&main]`                       | Print 4 longs at start of main in hex format. |
| `x/gf [&gd1]`                         | Print double.                                 |
| `help x`                              | Show formats for x.                           |
| `info locals`                         | Print local automatics only.                  |
| `info functions [regular expression]` | Print function names.                         |
| `info variables [regular expression]` | Print global variable names.                  |
| `ptype [expression]`                  | Print type definition.                        |
| `whatis [expression]`                 | Print type of expression.                     |
| `set [variable] = [expression]`       | Assign value.                                 |
| `display [expression]`                | Display expression result at stop.            |
| `undisplay`                           | Delete displays.                              |
| `info display`                        | Show displays.                                |
| `show values`                         | Print value history.                          |
| `info history`                        | Print value history.                          |