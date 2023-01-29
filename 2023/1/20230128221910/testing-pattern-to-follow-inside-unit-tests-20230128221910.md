---
path: '/2023/1/testing-pattern-to-follow-inside-unit-tests-20230128221910'
title: 'testing pattern to follow inside unit tests'
date: '20230128221910'
category: 'testing'
tags: ['mocks', 'pattern']
---

# testing pattern to follow inside unit tests
This is a pattern that I use quite heavily when writing my tests. I find this
helps to organize each unit test's setup, execution, and assertions.

I remember reading/hearing this from somewhere, but that reference may be lost to time.

## Tests follow the following flow
1. Arrange
1. Mock
1. Act
1. Assert

## Example test

```python

def my_func(var_one: int, var_two: int) -> int:
    return var_one + var_two


def test_my_func() -> None:

    # Arrange
    var_one = 1
    var_two = 1
    expected = 2

    # Mock
    # No behavior mocking required

    # Act
    result = my_func(var_one, var_two)

    # Assert
    assert result == expected

```

