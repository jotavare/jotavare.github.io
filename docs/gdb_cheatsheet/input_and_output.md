---
title: Input and Output
nav_order: 13
layout: default
parent: 📑 GDB Cheatsheet
---

## **INPUT AND OUTPUT**

| Command                         | Result                                                                     |
| :------------------------------ | :------------------------------------------------------------------------- |
| `info terminal`                 | Displays information recorded about the terminal modes.                    |
| `run > outfile`                 | Starts your program, diverting its output to the file outfile.             |
| `tty /dev/ttyb`                 | Default processes to do input and output on the terminal /dev/ttyb.        |
| `set inferior-tty [tty]`        | Set the tty for the program being debugged to tty.                         |
| `show inferior-tty`             | Show the current tty for the program being debugged.                       |
| `attach process-id`             | Attach to a running process that was started outside gdb.                  |
| `set exec-file-mismatch [ask]`  | Display a warning and ask the user whether to load the process executable. |
| `set exec-file-mismatch [warn]` | Just display a warning.                                                    |
| `set exec-file-mismatch [off]`  | Don’t attempt to detect a mismatch.                                        |
| `show exec-file-mismatch`       | Show the current value of exec-file-mismatch.                              |
| `detach`                        | Release the attached process from gdb control.                             |
| `kill`                          | Kill the child process in which your program is running.                   |