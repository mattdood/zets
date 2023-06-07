---
path: '/2023/6/redshift-useful-query-metrics-and-logging-internal-tables-20230607100258'
title: 'redshift useful query metrics and logging internal tables'
date: '20230607100258'
category: 'databases'
tags: ['redshift', 'tuning', 'queries', 'dba']
---

# redshift useful query metrics and logging internal tables
Redshift has quite a few internal tables that are good for viewing information about
your cluster's usage patterns. I found this to be particularly useful for determining
load on specific queries over time, because these tables are more granular than
the AWS Console.

## References
- [SVL Query metrics](https://docs.aws.amazon.com/redshift/latest/dg/r_SVL_QUERY_METRICS_SUMMARY.html) - Good for the
metrics but does not have timestamps. Keeps ~6 days of activity on a "reasonably active server".
- [STL Query metrics](https://docs.aws.amazon.com/redshift/latest/dg/r_STL_QUERY_METRICS.html) - Deeper detail
of the same table, but still does not have timestamps.
- [STL Query](https://docs.aws.amazon.com/redshift/latest/dg/r_STL_QUERY.html) - Raw data used in the previous
two tables, good and has timestamps.
- [Datetime abbreviations reference](https://docs.aws.amazon.com/redshift/latest/dg/r_FORMAT_strings.html)

