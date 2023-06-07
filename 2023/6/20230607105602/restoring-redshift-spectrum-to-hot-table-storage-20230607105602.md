---
path: '/2023/6/restoring-redshift-spectrum-to-hot-table-storage-20230607105602'
title: 'restoring redshift spectrum to hot table storage'
date: '20230607105602'
category: 'databases'
tags: ['dba', 'redshift', 'redshift spectrum', 'data lake', 'lakehouse']
---

# restoring redshift spectrum to hot table storage
Creating Redshift Spectrum tables is a great way to get data into a "lake"
while also ensuring it is query-able. This would be a "lakehouse", effectively,
a looking glass into the unstructured/hardly structured data that is stored in S3.

A great way to get data restored from Spectrum -> "hot" or "live" storage would
be to do this:

```sql
/*
*       title: Redshift Spectrum -> Live table
*       description: Loads data from Spectrum to a live
            internal Redshift table.
*/
SELECT
    *                                             -- Your columns
INTO <internal schema name>.<internal table name> -- Your destination
FROM <spectrum schema name>.<spectrum table name> -- Your source table
-- Optionally:
-- WHERE  -- Some filter
```

This does a $0.05/TB of data scanned query to insert data from the "read only"
Lake (S3 or similar) into the Redshift managed storage.
