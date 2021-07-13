---
path: '/2021/7/django-linebreaksbr-20210713120842'
title: 'django linebreaksbr'
date: '20210713120842'
category: 'django'
tags: ['python', 'django', 'frontend']
---

# django linebreaksbr
During some client work my friend and I ran into an issue where we didn't want a
full "rich text" style on a Django template (the client uses WagTail), but instead
just show linebreak/carriage returns in a `<p>` element.

This can be accomplished in two ways:
1. Showing a `|linebreaks` which changes the displays to blocks
1. Showing a `|linbreaksbr` which changes the carriage returns to `<br>` elements

[Link to the StackOverflow we found](https://stackoverflow.com/questions/2316028/how-to-print-line-breaks-in-python-django-template)

Example intended result:
```
This text would have a

linebreak
```

Actual display:
```
This text would have a linebreak
```

Changing the display:
```html
<div>
    <p>
        {{ some_text|linebreaksbr}}
    </p>
</div>
```

