---
title: Multiple Threads
nav_order: 15
layout: default
parent: GDB Cheatsheet
grand_parent: Cheatsheets
---

# **MULTIPLE THREADS**

| Command                                 | Result                                                                          |
| :-------------------------------------- | :------------------------------------------------------------------------------ |
| `thread [id]`                           | Switch among threads.                                                           |
| `info threads`                          | Inquire about existing threads.                                                 |
| `info threads [-gid] [thread-id-list]`  | Display information about one or more threads.                                  |
| `thread apply [thread-id-list] args`    | Apply a command to a list of threads.                                           |
| `maint info sol-threads`                | Display info on Solaris user threads.                                           |
| `thread apply [thread-id-list] command` | Apply the named command to one or more threads.                                 |
| `[-c]`                                  | Display errors and the execution of the thread apply then continues.            |
| `[-s]`                                  | Errors or empty output produced by a command to be silently ignored.            |
| `[-q]`                                  | Disables printing the thread information.                                       |
| `thread apply all -ascending command.`  | Apply a command to all threads in ascending order.                              |
| `taas [option]... command`              | Applies command on all threads, ignoring errors and empty output.               |
| `tfaas [option]... command`             | Applies command on all frames of all threads, ignoring errors and empty output. |
| `thread name [name]`                    | Assign a name to the current thread.                                            |
| `thread find [regexp]`                  | Search for and display thread ids whose name or systag matches.                 |
| `set print thread-events [on/off]`      | Print messages when new threads have started or exited.                         |
| `show print thread-events`              | Show whether messages will be printed when threads have started and exited.     |
| `set libthread-db-search-path [path]`   | List of directories gdb will use to search for libthread_db.                    |
| `show libthread-db-search-path`         | Display current libthread db search path.                                       |
| `set debug libthread-db [1/0]`          | Set the debug libthread-db as on or off.                                        |
| `show debug libthread-db`               | Display of libthread_db-related events.                                         |
| `set debug threads [on/off]`            | Set the debug threads as on or off.                                             |
| `show debug threads`                    | Print additional messages when threads are created and deleted.                 |