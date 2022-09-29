---
path: '/2022/9/installing-and-enabling-postgres-extensions-20220929123240'
title: 'installing and enabling postgres extensions'
date: '20220929123240'
category: 'databases'
tags: ['postgres', 'extensions', 'maintenance']
---

# installing and enabling postgres extensions
Working with Postgres extensions can be a little annoying when using Terraform.
I've learned recently that the extensions (once enabled) aren't actually **installed**
upon making revisions to the database.

In some cases when altering a [database parameter group setting](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithParamGroups.html)
in Terraform we have to use an `apply_method` that dictates the application of the setting.
When working with extensions in Postgres we also have to **run an extensions
script to fully install it**. This portion is not managed by Terraform or AWS (unfortunately).

Example Terraform parameter group:
```terraform
resource "aws_db_parameter_group" "sample_group" {
    parameter {
        name         = "shared_preload_libraries"
        value        = "pg_stat_statements"
        apply_method = "pending-reboot"
    }
}
```

## Checking installation of libraries
A query to check that the library was installed:

```sql
SELECT
    *
FROM
    pg_available_extensions
WHERE
    name = '<your library here>'
    AND
    installed_version IS NOT NULL;
```

Checking all installed libraries:

```sql
SELECT
    *
FROM
    pg_available_extensions
WHERE
    installed_version IS NOT NULL;
```

