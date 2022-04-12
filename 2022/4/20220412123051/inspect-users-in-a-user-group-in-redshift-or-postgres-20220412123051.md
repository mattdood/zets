---
path: '/2022/4/inspect-users-in-a-user-group-in-redshift-or-postgres-20220412123051'
title: 'inspect users in a user group in redshift or postgres'
date: '20220412123051'
category: 'redshift'
tags: ['dba', 'databases', 'redshift', 'aws', 'users', 'postgres']
---

# inspect users in a user group in redshift or postgres
To inspect information about our database/the engine itself we often will
query Postgres (RedShift) specific internal tables.

Inspecting our users that belong to a specific group:

```sql
SELECT
    usename,
    pg_group.groname
FROM
    pg_user,
    pg_group
WHERE
    pg_user.usesysid = ANY(pg_group.grolist)
    AND
    pg_group.groname='your-group-name';
```

