---
path: '/2023/6/redshift-serverless-is-poorly-documented-and-difficult-to-cost-analyze-20230607100803'
title: 'redshift serverless is poorly documented and difficult to cost analyze'
date: '20230607100803'
category: 'databases'
tags: ['redshift', 'dba', 'serverless', 'cost analysis']
---

# redshift serverless is poorly documented and difficult to cost analyze
Cost analysis for determining whether or not to swap to Redshift Serverless
is a horribly difficult process.

I have found that the documentation on the newly created service doesn't accurately
describe the computational throughput of the cluster vs. the cost.

This is due to some non-standardized units that we have to use to **guess** how
much Redshift Serverless would cost.

I used the below references and queries to analyze the Redshift Serverless estimated
costs for a given 1 day period to determine if there would be benefits from swapping
a cluster to that node type. This analysis was done due to the lack of clarity
around pricing and RPU capacity units.

## Useless references
These references are ones that were not helpful for analysis, unfortunately
they are from Amazon directly.
- [Serverless capacity](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-capacity.html) - Does not mention
actual "units" defined in comparison to current Redshift cluster node types.
- [Known issues, a dead link](https://docs.aws.amazon.com/redshift/latest/mgmt/working-with-serverless.html#serverless-known-issues) - Does
not have any information on actual issues, it appears to be a dead link.
- [Other known issues](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-known-issues.html) - This gives a few considerations
like migrations, query time, etc. but doesn't give any considerations on **capacity differences**

## Useful references
These are references that were used to create a comprehensive comparison in **cost**
between Redshift and Redshift Serverless based upon 1 day of "average usage".
- [Amazon Redshift Serverless CPU and RAM](https://chariotsolutions.com/blog/post/first-look-at-amazon-redshift-serverless/) - Discusses the "RPU"
comparison as being 2 vCPU and 16GB RAM, but only used 5-20s long queries to test the new capacity units
- [Sambaiz Athan vs. Redshift Serverless](https://www.sambaiz.net/en/article/397/) - Used Athena to do a comparison of cost between Athena and Redshift
Serverless, but did only smaller sized queries and with very little data. This is understandable, but difficult to extrapolate from.
Did not use cross-comparison of RPU sizing.
- [Amazon Redshift Serverless with Spectrum](https://chariotsolutions.com/blog/post/first-look-at-amazon-redshift-serverless/) - Found this to state that
Spectrum couldn't be used with Serverless, but in the documentation on AWS it is available. This may be out of date (same as first link).

## An "average day" query for comparisons
Due to the difficulty understanding the "RPU" capacity unit vs. the cost vs. # seconds
queries run (the pricing for our Serverless cluster), using a query to get "an average day"
at a glance was necessary.

To use these 2 queries, run them on an AWS Redshift cluster with recent activity.
**Note:** Be sure to change the timeframe we're filtering by.

### RPU capacity vs. estimated query cost
Query cost per RPU capacity is broken into query execution (CPU time) at different capacities.
32 RPUs is the lowest allowed capacity at time of writing, so this would be the "lowest cost"
to run the given query.
```sql
/*
*       title: Query cost by RPU for X days
*       description: Sets 32, 128, and 256 RPU units for Redshift
            Serverless cost analysis. Gives a cost per query view
            for previously executed queries in the last X days.
*/
SELECT
    TRIM(sq.querytxt) AS sql_query,
    qm.query_cpu_time,
    --        CPU TIME * COMPUTE RPUS * Cost/hr / seconds in a day
    qm.query_cpu_time * 32 * 0.375 / 3600 AS total_query_cost_32,
    qm.query_cpu_time * 128 * 0.375 / 3600 AS total_query_cost_128,
    qm.query_cpu_time * 256 * 0.375 / 3600 AS total_query_cost_256,
    qm.query_blocks_read,
    qm.query_execution_time,
    qm.query_cpu_usage_percent
FROm SVL_QUERY_METRICS_SUMMARY qm
LEFT JOIN stl_query sq ON qm.query = sq.query
WHERE
    qm.query_cpu_time > 0
    AND TRUNC(TO_DATE(sq.starttime, 'YYYY-MM-DD HH24:MI:SS.MS')) >= '2023-06-05'  -- Change here
    AND TRUNC(TO_DATE(sq.starttime, 'YYYY-MM-DD HH24:MI:SS.MS')) <= '2023-06-06'  -- Change here
    AND SUBSTRING(sq.querytxt, 1, 6) <> 'Vacuum'  -- EXCLUDE VACUUM operations because serverless won't need it?
    AND SUBSTRING(sq.querytxt, 1, 12) <> 'Auto Analyze'  -- EXCLUDE AUTO ANALYZE
    AND SUBSTRING(sq.querytxt, 1, 13) <> 'Alter Distkey'  -- EXCLUDE ALTER DISTKEY
ORDER BY qm.query_cpu_time DESC
```

### Summarized RPU capacity costs
Using a similar query to the above, we can get a summarized cost-basis for a given
timeframe's activity. This would be using the actual query executions we've had
on the existing cluster to predict the estimated cost given different RPU capacities.

```sql
/*
*       title: Query cost by RPU for X days summarized
*       description: Sets 32, 128, and 256 RPU units for Redshift
            Serverless cost analysis. Gives a cost per query view
            for previously executed queries in the last X days.
*/
SELECT
    SUM(qm.query_cpu_time) AS total_cpu_time_seconds,
    SUM(qm.query_cpu_time * 32 * 0.375 / 3600) AS total_query_cost_32,
    SUM(qm.query_cpu_time * 128 * 0.375 / 3600) AS total_query_cost_128,
    SUM(qm.query_cpu_time * 256 * 0.375 / 3600) AS total_query_cost_256
FROM SVL_QUERY_METRICS_SUMMARY qm
LEFT JOIN stl_query sq ON qm.query = sq.query
WHERE
    qm.query_cpu_time > 0
    AND TRUNC(TO_DATE(sq.starttime, 'YYYY-MM-DD HH24:MI:SS.MS')) >= '2023-06-05'  -- Change here
    AND TRUNC(TO_DATE(sq.starttime, 'YYYY-MM-DD HH24:MI:SS.MS')) <= '2023-06-06'  -- Change here
    AND SUBSTRING(sq.querytxt, 1, 6) <> 'Vacuum'  -- EXCLUDE VACUUM operations because serverless won't need it?
    AND SUBSTRING(sq.querytxt, 1, 12) <> 'Auto Analyze'  -- EXCLUDE AUTO ANALYZE
    AND SUBSTRING(sq.querytxt, 1, 13) <> 'Alter Distkey'  -- EXCLUDE ALTER DISTKEY
```
