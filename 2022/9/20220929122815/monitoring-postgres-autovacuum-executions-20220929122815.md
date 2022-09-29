---
path: '/2022/9/monitoring-postgres-autovacuum-executions-20220929122815'
title: 'monitoring postgres autovacuum executions'
date: '20220929122815'
category: 'databases'
tags: ['postgres', 'maintenance']
---

# monitoring postgres autovacuum executions

Recently when working with Postgres I had been tweaking some autovacuum settings
to better assist in table maintenance. To monitor the changes in tables
(how often they were autovacuumed) I ran the following query.

For more information on [autovacuum check the following reference](https://www.postgresql.org/docs/current/routine-vacuuming.html).

```sql
SELECT
    relname,
    last_vacuum,
    last_autovacuum,
    last_analyze,
    last_autoanalyze
FROM
    pg_stat_user_tables;
```

