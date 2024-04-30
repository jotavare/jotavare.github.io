---
title: Layout
nav_order: 4
layout: default
parent: 📑 GDB Cheatsheet
---

## **LAYOUT**

| Command                             | Result                                                                        |
| :---------------------------------- | :---------------------------------------------------------------------------- |
| `layout next`                       | Display the next layout.                                                      |
| `layout prev`                       | Display the previous layout.                                                  |
| `layout src`                        | Display the source window only.                                               |
| `layout asm`                        | Display the assembly window only.                                             |
| `layout split`                      | Display the source and assembly window.                                       |
| `layout regs`                       | Display the register window together with the source or assembly window.      |
| `focus next`                        | Make the next window active for scrolling.                                    |
| `focus prev`                        | Make the previous window active for scrolling.                                |
| `focus src`                         | Make the source window active for scrolling.                                  |
| `focus asm`                         | Make the assembly window active for scrolling.                                |
| `focus regs`                        | Make the register window active for scrolling.                                |
| `focus cmd`                         | Make the command window active for scrolling.                                 |
| `refresh`                           | Refresh the screen. This is similar to typing `CTRL` + `L` or `ref`.          |
| `tui reg float`                     | Show the floating point registers in the register window.                     |
| `tui reg general`                   | Show the general registers in the register window.                            |
| `tui reg system`                    | Show the system registers in the register window.                             |
| `tui reg next`                      | Show the next register group. List register groups as well as their order.    |
| `update`                            | Update the source window and the current execution point.                     |
| `info win`                          | List and give the size of all displayed windows.                              |
| `winheight [layout] [+-number]`     | Change the height of the window name by lines (+ increase and - decreases).   |
| `tabset [nchars]`                   | Set the width of tab stops to be nchars characters.                           |
| `set height lpp`                    | Specify a screen height of lpp lines.                                         |
| `show height`                       | Show current screen height.                                                   |
| `set width cpl`                     | Specify a screen width of cpl characters.                                     |
| `show width`                        | Show current screen width.                                                    |
| `tui reg float`                     | Show the floating point registers in the register window.                     |
| `tui reg system`                    | Show the system registers in the register window.                             |
| `tui reg general`                   | Show the general registers in the register window.                            |
| `set pagination [on/off]`           | Turn the output pagination on or off. Turning pagination off = `set height 0` |
| `show pagination`                   | Show the current pagination mode.                                             |
| `set tui border-kind [kind]`        | Select the border appearance for the source, assembly and register windows.   |
| `[space]`                           | Use a space character to draw the border.                                     |
| `[ascii]`                           | Use ascii characters `+`, `-` and `\|` to draw the border.                    |
| `[acs]`                             | Use the Alternate Character Set to draw the border.                           |
| `[drawn]`                           | Using character line graphics if the terminal supports them.                  |
| `set tui border-mode [mode]`        | Select the display attributes for the inactive window border.                 |
| `set tui active-border-mode [mode]` | Select the display attributes for the active window border.                   |
| `[standout]`                        | Use standout mode.                                                            |
| `[reverse]`                         | Use reverse video mode.                                                       |
| `[half]`                            | Use half bright mode.                                                         |
| `[half-standout]`                   | Use half bright and standout mode.                                            |
| `[bold]`                            | Use extra bright or bold mode.                                                |
| `[bold-standout]`                   | Use extra bright or bold and standout mode.                                   |