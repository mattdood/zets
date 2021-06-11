|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| custom-django-admin-filters | django  | django admin  | 20210610221136 |

# custom django admin filters
Today I had the need to provide a custom filter to users of the Django admin page.

I found that the model I was working with was the parent of several child models
which made this a bit tricker to implement. This would be to filter models for
a multi-tenant application that had different child models for each of the sites.

There was a great StackOverflow post regarding extending the `SimpleListFilter`
from Django.

**Sample implementation:**

```python

from django.contrib import admin

class SiteFilter(admin.SimpleListFilter):
    """Custom multi-site admin filter.

    The models are extended on a per-site
    basis and require being back-filtered into
    the parent model.
    """
    title = 'site'
    parameter_name = 'site'

    def lookups(self, request, model_admin):
        SITE_ONE = 'site_one'
        SITE_TWO = 'site_two'
        SITE_THREE = 'site_three'

        SITES = [
            (SITE_ONE, 'Site One'),
            (SITE_TWO, 'Site Two'),
            (SITE_THREE, 'Site Three'),
        ]
        return SITES

    def queryset(self, request, queryset):
        from some.models import SiteOne, SiteTwo, SiteThree

        if self.value() == 'site_one':
            site_one_objects = SiteOne.objects.your().filters()
            return queryset.filter(id__in=site_one_objects)
        if self.value() == 'site_two':
            site_two_objects = CatalystArticle.objects.your().filters()
            return queryset.filter(id__in=site_two_objects)
        if self.value() == 'site_three':
            site_three_objects = FinfeedArticle.objects.your().filters()
            return queryset.filter(id__in=site_three_objects)

```
