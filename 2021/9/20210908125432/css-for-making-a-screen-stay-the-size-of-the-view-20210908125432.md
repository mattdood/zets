---
path: '/2021/9/css-for-making-a-screen-stay-the-size-of-the-view-20210908125432'
title: 'css for making a screen stay the size of the view'
date: '20210908125432'
category: 'css'
tags: ['html', 'css']
---

# css for making a screen stay the size of the view
Making a screen avoid overflow when creating a single page app that should behave
like an OS would was annoying. I found this CSS tidbit that I'd like to remember.

The idea is that this will keep any draggable content from resizing the screen
if it overflows an edge. This helps with usability and makes the entire experience
a lot cleaner.

```css
html,
body {
  height: 100%;
}

body {
  overflow: hidden;
}
```

