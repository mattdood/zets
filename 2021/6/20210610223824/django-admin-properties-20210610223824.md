---
title: 'Django Admin Properties'
date: '20210610223824'
category: 'django'
tags: ['django admin', 'models', 'python']
---

# django admin properties
When working in the Django admin today I created a custom property that displays
for the backend user. I previously had not tried to display a model property
in the admin; however, it is the same as a regular model column.

Also, I used `@cached_property` to keep a cache of the instance rather than
recomputing this every call.

A generic example:

```python

# models.py
from django.utils.functional import cached_property

class SomeModel(models.Model):
    some_word = models.CharField(max_length=5)
    some_bool = models.BooleanField(default=False)

    @cached_property
    def is_word(self):
        return True if 'word' == self.some_word else False


# admin
class SomeModelAdmin(admin.ModelAdmin):
    list_display = ['some_word', 'some_bool', 'is_word']

```
