---
path: '/2022/5/postgres-table-constraint-definitions-from-pg_constraint-20220520125323'
title: 'postgres table constraint definitions from pg_constraint'
date: '20220520125323'
category: 'databases'
tags: ['postgres', 'dba']
---

# postgres table constraint definitions from pg_constraint
The constraints feature of Postgres table columns is a great way to provide data
validation from a database perspective.

To retrieve the constraints listed within a schema we can utilize the following
query from [StackOverflow regarding constraint checking](https://stackoverflow.com/questions/67999205/postgres-check-constraint-definition)

```sql
c = check constraint
f = foreign key constraint
p = primary key constraint
u = unique constraint
t = constraint trigger
x = exclusion constraint

select pgc.conname as constraint_name,
       ccu.table_schema as table_schema,
       ccu.table_name,
       ccu.column_name,
       pg_get_constraintdef(pgc.oid)
from pg_constraint pgc
join pg_namespace nsp on nsp.oid = pgc.connamespace
join pg_class  cls on pgc.conrelid = cls.oid
left join information_schema.constraint_column_usage ccu
          on pgc.conname = ccu.constraint_name
          and nsp.nspname = ccu.constraint_schema
where contype ='c'
order by pgc.conname;
```

## Altering existing constraints
We can't actually `ALTER` a constraint on the table, they have to be dropped then
re-added.

```sql
ALTER TABLE schema_name.table_name
    DROP CONSTRAINT constraint_name;
ALTER TABLE schema_name.table_name
    ADD CONSTRAINT constraint_name CHECK
        <your validation>;
```

