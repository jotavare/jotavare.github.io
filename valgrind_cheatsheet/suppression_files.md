---
title: Suppression Files
nav_order: 6
layout: default
parent: Valgrind Cheatsheet
---

# **SUPPRESSION FILES**

<div class="code-example" markdown="1">
Ignore errors of given types and locations in file `mysuppressions.supp`.
</div>
```shell
valgrind --suppressions=myerrors.supp [--tool=... ]
```
 
<div class="code-example" markdown="1">
Print a suppression for each error, for copying to a suppression file.
</div>
```shell
valgrind --gen-suppressions=yes [--tool=... ]
```

```shell
myerrors.supp
{
__gconv_transform_ascii_internal/__mbrtowc/mbtowc
    Name identifying this entry.
Memcheck:Value4
    Error given by Memcheck tool. Uninitialized value of width 4 bytes.
fun:__gconv_transform_ascii_internal
fun:__mbr*toc
fun:mbtowc
    Call stack matches these three functions in order. Note the wildcard.
}
Example entry in a suppression file. It applies if all the conditions are met.
```

{: .important-title }
Valgrind also ignores known errors in system libraries on many systems. On others, you may need a lot of suppression wildcards for library errors.