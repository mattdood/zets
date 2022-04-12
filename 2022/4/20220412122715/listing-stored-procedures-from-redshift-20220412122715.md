---
path: '/2022/4/listing-stored-procedures-from-redshift-20220412122715'
title: 'listing stored procedures from redshift'
date: '20220412122715'
category: 'redshift'
tags: ['dba', 'databases', 'redshift', 'aws', 'stored procedure']
---

# listing stored procedures from redshift
Finding if a stored procedure is in the proper schema is sometimes important for
troubleshooting what something was created against. This is true for all database
engines (Postgres, MSSQL, RedShift, etc.) and is important to be comfortable checking in on.

I've found that the stored procedures will sometimes be created in a public schema
or a `pg_catalog` specific schema.

To check, I utilize this [query from StackOverflow](https://stackoverflow.com/a/66668507):

```sql
SELECT
    n.nspname AS function_schema,
    p.proname AS function_name
FROM
    pg_proc p
LEFT JOIN pg_namespace n ON p.pronamespace = n.oid
WHERE
    n.nspname NOT IN ('pg_catalog', 'information_schema')
    AND
    p.proname ILIKE '%your-procedure-name%'
ORDER BY
    function_schema,
    function_name;
```

