---
path: '/2021/11/django-create-secondary-model-on-create-20211114215019'
title: 'django create secondary model on create'
date: '20211114215019'
category: 'django'
tags: ['python']
---

# django create secondary model on create
When working in Django if you have related models that require an on-create
feature to generate a child you can utilize the `post_save` callbacks.

This is especially useful when we want to generate the secondary model using
information largely irrelevant to the parent model.

One instance would be a `User` model parent that has a child model holding its
state. This state could be a `Profile` of additional information, some sort of
`Organization` model that has account payment status, etc.

By generating this on `User` create we would be able to have a secondary representation
of the `User` without having to do any complex callbacks/checks to ensure they
have this data representation.

Ideally, we would be creating this child model with some default values.

```python
@receiver(post_save, sender=User)
def create_your_model(sender, instance, created, **kwargs):
    if created:
        SomeModel.objects.create(your_foreign_key_field=instance)


@receiver(post_save, sender=User)
def save_your_model(sender, instance, **kwargs):
    instance.somemodel.save()
```

