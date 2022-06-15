---
path: '/2022/6/converting-iso-varchar-dates-to-date-types-in-postgres-20220615150533'
title: 'converting iso varchar dates to date types in postgres'
date: '20220615150533'
category: 'databases'
tags: ['postgres', 'iso', 'timestamps']
---

# converting iso varchar dates to date types in postgres
Working with date conversions in SQL can be pretty tedious. Today I was working
on a data pull and needed to convert a `VARCHAR` type to a `DAY` to make things
more manageable for a `GROUP BY` clause.

In doing so, I ran into a scenario where my dates were coming out incorrect. I noticed
that the date format I used was improper, and the Postgres engine doesn't use the
same shorthand for date types that I was used to.

Example:
```
"2022-06015 13:00:00" -> 2022-06-15
```

The SQL for the above conversion would be:
```SQL
SELECT
    TRUNC(TO_DATE(<your-varchar-column>, 'YYYY-MM-DD HH24:MI:SS')) AS DAY
FROM <your-table>
```

[Here's a reference for date types in Postgres.](https://www.postgresql.org/docs/current/functions-formatting.html)

