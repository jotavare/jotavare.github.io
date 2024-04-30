---
title: Browsing Source
nav_order: 7
layout: default
parent: 📑 GDB Cheatsheet
---

## **BROWSING SOURCE**

| Command                               | Result                                  |
| :------------------------------------ | :-------------------------------------- |
| `list [20]`                           | List 10 lines around line `20`.         |
| `list [1,10]`                         | List lines `1` to `10`.                 |
| `list [main]`                         | List lines around function `main`.      |
| `list [basic.c:main]`                 | List from another file `basic.c`.       |
| `list -`                              | List previous 10 lines.                 |
| `info address [Symbol name]`          | Displays the address of a given symbol. |
| `list [*0x22e4]`                      | List source at address `p0x22e4`.       |
| `cd [dir]`                            | Change current directory to `dir`.      |
| `pwd`                                 | Print working directory.                |
| `search [regular expression]`         | Forward search for regular expression.  |
| `reverse-search [regular expression]` | Backward search for regular expression. |
| `dir [dirname]`                       | Add directory `dirname` to source path. |
| `dir`                                 | Reset source path to nothing.           |
| `show directories`                    | Show source path.                       |