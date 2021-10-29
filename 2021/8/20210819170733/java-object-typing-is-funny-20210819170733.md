---
path: '/2021/8/java-object-typing-is-funny-20210819170733'
title: 'java object typing is funny'
date: '20210819170733'
category: 'java'
tags: ['funny', 'oop']
---

# java object typing is funny
Jordan was creating a JavaFX project and needed to determine the type of one
of the objects he was interacting with. Coming from a Python background we
were prepared for something funny; however, the code was a joke-worthy string
of function calls.

```java
// Getting the object type of a
// JavaFX object
String name = sourceList.getSelectionModel().getSelectedItem().getClass().getSimpleName();
System.out.print(name);

// Getting the object type of a
// regular Java object
String name = someObject.getClass().getSimpleName();
System.out.print(name);

```

In contrast, Python is a bit simpler...

```python

some_object = Object()

type(some_object)

```

