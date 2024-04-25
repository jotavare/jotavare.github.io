---
title: Running The Program
nav_order: 1
layout: default
parent: GDB Cheatsheet
---

# RUNNING THE PROGRAM

<div>
<table>
<tr><th></th>
<tr><td>
  
| Command                               | Result                                             |
| :------------------------------------ | :------------------------------------------------- |
| `gdb`                                 | Start gdb.                                         |
| `gdb --tui [object]`                  | Start gdb with graphic interface.                  |
| `gdb -silent`                         | Start gdb without the beginning information.       |
| `gdb -statistics`                     | Print statistics about time and memory usage.      |
| `gdb [object]`                        | Normal debug.                                      |
| `gdb [object] [core]`                 | core debug (must specify core file).               |
| `gdb [object] [pid]`                  | Attach to a running process.                       |
| `gdb [program] [core dump]`           | Start GDB (with optional core dump).               |
| `gdb --args [program] [args...]`      | Start GDB and pass arguments.                      |
| `gdb --pid [pid]`                     | Start GDB and attach to process.                   |
| `run`                                 | Run the program with current arguments.            |
| `run [args] [redirection]`            | Run with args and redirection.                     |
| `set args [args...]`                  | Set arguments for run.                             |
| `show args`                           | Show current arguments to run.                     |
| `cont`                                | Continue the program.                              |
| `step`                                | Single step the program, also step into functions. |
| `step [number of lines]`              | Step n number of lines.                            |
| `next`                                | Next line.                                         |
| `next [number of lines]`              | Next n number of lines.                            |
| `attach [process-id]`                 | Attach to running program.                         |
| `detach`                              | Detach from running program.                       |
| `define [command ...] end`            | Define user command.                               |
| `RETURN`                              | Repeat last command.                               |
| `shell [command] [args]`              | Execute shell command.                             |
| `source [file]`                       | Load gdb commands from file.                       |
| `quit`                                | Quit gdb.                                          |
| `finish`                              | Finish current function's execution.               |
| `kill`                                | Kill current executing program.                    |

</center>

</td></tr>
</table>
</div>