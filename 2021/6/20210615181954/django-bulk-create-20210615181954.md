|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| django-bulk-create | django  | django, postgres  | 20210615181954 |

# django bulk create
Bulk create operations are a faster, minimally logged operation that
reduces database traffic when doing bulk inserts.

[Bulk create documentation](https://docs.djangoproject.com/en/3.2/ref/models/querysets/#bulk-create)
[Django serialization docs](https://docs.djangoproject.com/en/3.2/topics/serialization/)

## Sample implementation
This implementation will use a `serialize()` and `deserialize()` example to show
additional extensibility not from the documentation.

I utilized `ignore_conflicts` because the model has a `unique` field and any
bad data shouldn't be saved and will just fail silently.

```python

def some_method(some_serialized_list):

    deserialized_data_list = [some_data.object
        for some_data in deserialize('json', some_serialized_list)]

    SomeModel.objects.bulk_create(deserialized_data_list, ignore_conflicts=True)

```
