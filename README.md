<p align="center">
	<img src="https://img.shields.io/badge/status-ongoing-success?color=%2312bab9&style=flat-square"/>
	<img src="https://img.shields.io/github/languages/top/jotavare/jotavare.github.io?color=%2312bab9&style=flat-square"/>
	<img src="https://img.shields.io/github/last-commit/jotavare/jotavare.github.io?color=%2312bab9&style=flat-square"/>
	<a href='https://www.linkedin.com/in/jotavare' target="_blank"><img alt='Linkedin' src='https://img.shields.io/badge/LinkedIn-blue?style=flat-square'/></a>
</p>

<p align="center">
	<a href="#about">About</a> •
	<a href="#contents">Contents</a> •
	<a href="#running-it-locally">Running it locally</a> •
	<a href="#building">Building</a> •
	<a href="#contributing">Contributing</a> •
	<a href="#note-on-diagrams">Diagrams</a> •
	<a href="#license">License</a>
</p>

## ABOUT

The source for [**jotavare.github.io**](https://jotavare.github.io/), a personal
documentation site built with [Jekyll](https://jekyllrb.com/) and the
[just-the-docs](https://just-the-docs.com/) theme, deployed with GitHub Pages.

It gathers notes I wanted in one searchable place rather than scattered across
repositories: cheatsheets for the tools I use and a longer set of x86 assembly
notes written while learning it.

## CONTENTS

| Section | Pages | What it covers |
| :-- | :-- | :-- |
| **GDB cheatsheet** | 19 | Breakpoints, stack and data inspection, TUI layout, threads, forks and machine-level debugging |
| **Valgrind cheatsheet** | 7 | Memcheck, Helgrind, leak kinds, suppression files and reading the common errors |
| **x86 Assembly (NASM)** | 39 | Binary basics, registers and EFLAGS, data and memory, operations, procedures, file handling, and building a small OS |
| **WPA-PSK** | 1 | A walkthrough of the handshake-capture word-list attack, for authorised testing only |

The rendered site nests these under a searchable sidebar; the tables above are
the top-level shape.

## RUNNING IT LOCALLY

```bash
git clone https://github.com/jotavare/jotavare.github.io.git
cd jotavare.github.io
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000/`. You need Ruby (the deploy pins **3.3**) and
Bundler.

## BUILDING

```bash
bundle exec jekyll build
```

Output goes to `_site/`. On every push to `main`, GitHub Actions builds the same
way and deploys to Pages; pull requests are built by a separate workflow but not
deployed.

## CONTRIBUTING

This is a personal reference and is not open to changes. Spotting a factual
error in the notes is welcome, but issues are disabled, so there is nothing to
act on a report with.

## NOTE ON DIAGRAMS

Some of the diagrams under `assets/images/` come from external sources and are
included for reference; where the original author is known they are credited on
the page, and the rest are marked as external. They are not my own work.

## LICENSE

This project is available under the MIT License. For further details, please refer to the [LICENSE](https://github.com/jotavare/jotavare.github.io/blob/main/LICENSE) file.
