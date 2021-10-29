---
path: '/2021/8/react-object-events-and-what-to-link-with-20210819180531'
title: 'react object events and what to link with'
date: '20210819180531'
category: 'javascript'
tags: ['react', 'gatsbyjs']
---

# react object events and what to link with
During my personal site revamp I started learning React and noticed that I had
some errors when I was trying to assign a link to a `<div>`. These were
both the linting and functional errors regarding what we "should" do to elements.

After reading up I found a few StackOverflow posts that correctly describe the
behavior we should have.

Posts:
1. [Overall explanation](https://stackoverflow.com/a/54612218/12387496)
1. [Keyboard listeners](https://stackoverflow.com/questions/48575674/how-to-add-a-keyboard-listener-to-my-onclick-handler)
1. [Event handlers](https://stackoverflow.com/questions/42225468/static-elements-interactions)

Loose rendition of the code I was using:

```javascript
<div
  onClick={event => (navigate(/posts))}
>
```


Errors I received:

```bash
> Visible, non-interactive elements with click handlers must have at least one keyboard listener.
> Static HTML elements with event handlers require a role.
```

