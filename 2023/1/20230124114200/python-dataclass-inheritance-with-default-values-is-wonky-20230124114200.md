---
path: '/2023/1/python-dataclass-inheritance-with-default-values-is-wonky-20230124114200'
title: 'python dataclass inheritance with default values is wonky'
date: '20230124114200'
category: 'python'
tags: ['dataclass', 'inheritance']
---

# python dataclass inheritance with default values is wonky
Recently I had an opportunity to utilize Python the `@dataclass` to handle some
data that I wanted to behave similar to a `Struct` would in any other language.

The idea was I'd have a dataclass that held quite a few values that I needed to
pass around and return to another consumer of the data, but I wanted to avoid a
length `__init__()` with lots of arguments.

## Problems
Below are a few of the snafoos that I ran into when working with dataclasses. While
they're not dealbreakers, they were a bit interesting to work with and something
to consider when creating some reusable (and understandable) data representations.

### Instantiating without all the values
I immediately ran into a few issues with this, namely with instantiation of the
class requiring all values to be present when it was created. Now, this could
be remediated with default values - but I felt that defeated the purpose of
the implementation. This was especially the case when a few of my fields were
either calculated fields (relying on other data) or required some API calls to
populate.

I found that the best course of action here was to handle some `__post_init__()`
for those values that required special cases.

Example:

```python
from dataclasses import dataclass, field

@dataclass
class Example

    var_one: int
    var_two: int
    sum_one_two: int = field(init=False)

    def __post_init__(self) -> None:
        self.sum_one_two = self.var_one + self.var_two
```

### Inheritance with default values
Handling inheritance was an interesting issue, wherein the default values
of the parent class are not considered during instantiation due to the ordering
of how they're created.

* [Great StackOverflow explanation for this situation](https://stackoverflow.com/questions/51575931/class-inheritance-in-python-3-7-dataclasses)
    * The above post handles explaining instantiation order of default values
    within dataclass inheritance.

The above StackOverflow post boils down to:
* When you're using dataclass inheritance order matters first and foremost
* Default values are likely best placed in separate "base classes" to avoid
instantiation errors
* Default values should always be segmented away from any `__post_init__` processing
that you may have in our dataclasses

#### Naive solution to work around this
I found that the idea of having multiple dataclasses as a base/parent to inherit
from and separating default values to be a bit clunky.

To avoid this, I instead init the parent class first during the `__post_init__`
then handle the remainder of the non-default values for the child class.

In the below example we can see that our parent `Example` is initialized first,
has it's `__post_init__` run, then we handle the non-default/calculated fields.

If we were to avoid the `super().__post_init__()` we'd receive a "default comes before other fields"
error that indicates an instantiation problem.

```python
from dataclasses import dataclass, field

@dataclass
class Example

    var_one: int = 1
    var_two: int = 1
    sum_one_two: int = field(init=False)

    def __post_init__(self) -> None:
        self.sum_one_two = self.var_one + self.var_two


@dataclass
class ExampleChild(Example):

    var_three: int = 1
    sum_one_two_three: int = filed(init=False)

    def __post_init__(self) -> None:
        super().__post_init__()

        self.sum_one_two_three = self.sum_one_two + self.var_three
```

