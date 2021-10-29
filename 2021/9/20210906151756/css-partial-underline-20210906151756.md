---
path: '/2021/9/css-partial-underline-20210906151756'
title: 'css partial underline'
date: '20210906151756'
category: 'css'
tags: ['css']
---

# css partial underline
CSS and HTML do not inherently have the ability to do partial underlines.

In HTML we can use a `<u></u>` tag to do an underline, but this doesn't always
accomplish what we'd like to do with a given content block

In CSS we can use a `border` element to have a bit more control, but this would
also be subject to the size of the content block itself.

I found this StackOverflow example for a partial underline based on a set `width`
parameter that helps to do partials.

[Link to StackOverflow example, bottom of the answer](https://stackoverflow.com/a/37338297/12387496)

```css
.partial-underline {
  display: table;
}

.partial-underline:after {
  border-bottom: 1px solid #f00;
  content: '';
  display: block;
  margin-left: 25%;
  width: 50%;
}
```

Screenshot of an in-progress revamp I was using this on:


![A blue background with the word Stocks, header has 80% underline](./20210906152231-img-1.png)

This header has an 80% underline on it.

