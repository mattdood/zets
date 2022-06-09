---
path: '/2022/6/pydoc-is-great-and-i-should've-used-it-sooner-20220608215233'
title: 'pydoc is great and I should've used it sooner'
date: '20220608215233'
category: 'python'
tags: ['docs']
---

# pydoc is great and I should've used it sooner
I was recently watching an AnythonyWritesCode video (great content) and noticed
the command line assistance for Python documentation. I'm a bit embarassed to say
how long I've been accessing documentation via Google to look up builtin classes
or methods.

The syntax for a search is as follows:

```bash
python3 -m pydoc <your function or class>
```

An example of this would be:

```bash
python3 -m pydoc exit() # would print all of the documentation for an exit() call
```

To search this documentation you would use the built in search functionality of
the default editor your OS has. Mine is Vim, so I would use a `/<search string>`.

