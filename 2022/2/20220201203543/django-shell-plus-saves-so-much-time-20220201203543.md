---
path: '/2022/2/django-shell-plus-saves-so-much-time-20220201203543'
title: 'django shell plus saves so much time'
date: '20220201203543'
category: 'django'
tags: ['python', 'django', 'bash']
---

# django shell plus saves so much time
When working with the shell inside Docker containers during Django app development
often times it is tedious to work through imports back and forth during file changes.

Typically I would utilize the `shell` option in Django using this:
```bash
docker-compose run --rm web python manage.py shell
```

Then I would import my required files (models and whatnot) and work through
the tests or changes I needed.

This gets annoying when having to do it frequently, whereas we could instead use
the `shell_plus` module and get direct access to **all imports** for the whole
project.
```bash
docker-compose run --rm web python manage.py shell_plus
```

