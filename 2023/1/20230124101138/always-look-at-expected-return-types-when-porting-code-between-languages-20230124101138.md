---
path: '/2023/1/always-look-at-expected-return-types-when-porting-code-between-languages-20230124101138'
title: 'always look at expected return types when porting code between languages'
date: '20230124101138'
category: 'lessons'
tags: ['legacy code', 'python', 'golang']
---

# always look at expected return types when porting code between languages
When you're porting a project from one language to another, as a note to myself
I need to always take a look at the return structure of the original project.

It can be a little tedious to trace through to the exact return values, but it
helps to start at the end (the return value) then trace it backwards through
the legacy code.

This especially helps for in-place rewrites that cause a lot of heartache when
troubleshooting, as the systems that are still invoking it will not be aware
of the underlying change in the rewrite process.

