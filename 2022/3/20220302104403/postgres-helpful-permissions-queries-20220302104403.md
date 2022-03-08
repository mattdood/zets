---
path: '/2022/3/postgres-helpful-permissions-queries-20220302104403'
title: 'postgres helpful permissions queries'
date: '20220302104403'
category: 'postgres'
tags: ['dba', 'permissions', 'queries']
---

# postgres helpful permissions queries
When creating new users, schemas, and tables inside a PostgreSQL database instance
(usually in AWS RDS, though local Docker containers as well) it is pretty
cumbersome to remember permissions.

I typically use a least-privilege approach, which is why the users are provisioned
on an as-needed basis whenever new functionality is added to the system.

This could be when we create a new feature, new service in the application, or
have a separate external service.

Additionally, this would hold true for new team members or external department members
that require access.

## Useful queries
These queries are [pulled directly from this source](https://tableplus.com/blog/2018/04/postgresql-how-to-grant-access-to-users.html)
and I'm keeping them here for safe keeping.

How to grant access to users in PostgreSQL?
Here are some common statement to grant access to a PostgreSQL user:

1. Grant CONNECT to the database:
```
GRANT CONNECT ON DATABASE database_name TO username;
```

2. Grant USAGE on schema:
```
GRANT USAGE ON SCHEMA schema_name TO username;
```

3. Grant on all tables for DML statements: SELECT, INSERT, UPDATE, DELETE:
```
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA schema_name TO username;
```

4. Grant all privileges on all tables in the schema:
```
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA schema_name TO username;
```

5. Grant all privileges on all sequences in the schema:
```
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA schema_name TO username;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA schema_name TO username;
```

6. Grant all privileges on the database:
```
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
```

7. Grant permission to create database:
```
ALTER USER username CREATEDB;
```

8. Make a user superuser:
```
ALTER USER myuser WITH SUPERUSER;
```

9. Remove superuser status:
Those statements above only affect the current existing tables. To apply to newly created tables, you need to use alter default. For example:
```
ALTER USER username WITH NOSUPERUSER;

ALTER DEFAULT PRIVILEGES
FOR USER username
IN SCHEMA schema_name
GRANT SELECT, INSERT, UPDATE, DELETE ON TABLES TO username;
```

