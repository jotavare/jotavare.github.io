---
title: Multiple Inferiors Connections
nav_order: 14
layout: default
parent: GDB Cheatsheet
---

# **MULTIPLE INFERIORS CONNECTIONS**

| Command                              | Result                                                               |
| :----------------------------------- | :------------------------------------------------------------------- |
| `info inferiors`                     | Print a list of all inferiors currently being managed by gdb.        |
| `inferior`                           | Shows information about the current inferior.                        |
| `info connections`                   | Print a list of all open target connections currently being managed. | 
| `inferior [id]`                      | Make inferior [id] the current inferior.                             |
| `add-inferior`                       | Adds n inferiors to be run using executable as the executable.       |
| `[-copies n]`                        |                                                                      |
| `[-exec executable]`                 |                                                                      |
| `[-no-connection]`                   |                                                                      |
| `clone-inferior [-copies n] [id]`    | Adds n inferiors ready to execute the same program as inferior [id]. |
| `remove-inferiors [id]`              | Removes the inferior or inferiors.                                   |
| `detach inferior [id]`               | Detach from the inferior(s) identified by inferior [id].             |
| `kill inferiors [id]`                | Kill the inferior or inferiors identified by inferior [id].          |
| `set print inferior-events [on/off]` | Enable or disable printing of new inferiors.                         |
| `show print inferior-events`         | Print if inferiors have started, exited or have been detached.       |
| `maint info program-spaces`          | Print a list of all program spaces currently being managed.          |