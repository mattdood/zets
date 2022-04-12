---
path: '/2022/4/retrieve-table-size-stats-and-other-info-from-redshift-20220412123534'
title: 'retrieve table size stats and other info from redshift'
date: '20220412123534'
category: 'redshift'
tags: ['redshift', 'aws', 'dba', 'databases']
---

# retrieve table size stats and other info from redshift
Often times when looking at table performance, query efficiency, compression,
etc. we'll need to have a wholistic view of what is going on with the table itself.

This yields information about the underlying distribution, sorting style, size of the table,
and whether or not the stats should be updated, etc.

Using this query (**runs for a long time**) we're able to get an accurate look
at what we have in the cluster while giving us some information to use if we dive
deeper:

```sql
SELECT
  "schema",
  "table",
  size, -- MiB
  pct_used, -- % of storage
  diststyle,
  sortkey_num, -- similar to indexes
  stats_off, -- 0 = perfect stats (good), 100 = completely unordered stats (bad)
  tbl_rows,
  unsorted, -- % of data that isn't sorted
  vacuum_sort_benefit -- benefit of sorting
FROM svv_table_info
WHERE
    "table" = 'table-name-here'
    AND
    "schema" = 'schema-name-here'
ORDER BY 2, 6 DESC
```

