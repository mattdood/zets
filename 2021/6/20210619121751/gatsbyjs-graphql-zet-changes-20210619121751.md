---
title: 'gatsbyjs graphql zet changes'
date: '20210619121751'
category: 'zet'
tags: ['gatsbyjs', 'markdown', 'zet']
---

# gatsbyjs graphql zet changes
When working through how I'll be deploying my Zets to my website I found that the
typical parsing I was anticipating from the GatsbyJS tools was lackluster.

The parsing is stuck in a standardized format and is pretty difficult to get
ahold of to change. Previously I was pushing all Zets with a tabular format
that would have metadata pushed into it.

I've changed this to be in an adapted format, examples below.

Previous:
```
| Title | Category | Tags | Date |
| ----- | -------- | ---- | ---- |
| some title | category | tags, tags | 202101011212 |
```

Adapted:
```
---
title: 'some title'
date: 'date'
category: 'someCategory'
tags: ['some', 'tag']
---
```

