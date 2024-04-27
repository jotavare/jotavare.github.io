---
title: Types of Memory Leak
nav_order: 2
layout: default
parent: Valgrind Cheatsheet
---

## **TYPES OF MEMORY LEAK**

| Type | Description |
| :--- | :---------- |
| Reachable     | Not leaked, but not deallocated before exit.              |
| Lost          | Pointer deallocated without deallocating memory.          |
| Possibly Lost | Some part can be reached but not the start of the memory. |