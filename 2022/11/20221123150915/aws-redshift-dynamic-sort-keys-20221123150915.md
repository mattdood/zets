---
path: '/2022/11/aws-redshift-dynamic-sort-keys-20221123150915'
title: 'aws redshift dynamic sort keys'
date: '20221123150915'
category: 'databases'
tags: ['redshift', 'maintenance']
---

# aws redshift dynamic sort keys
Previously when working on Redshift clusters tables needed to be recreated
in order to change the sort key (how data is stored and analyzed by the query analyzer).

Now, as of 2019, we're able to work with tables to `ALTER SORT KEY` which will
force Redshift to adjust the data layout in the background while ensuring
the table is available for users to query.

* [Reference to the blog post](https://aws.amazon.com/about-aws/whats-new/2019/11/amazon-redshift-supports-changing-table-sort-keys-dynamically/)
* [Working with sort keys](https://docs.aws.amazon.com/redshift/latest/dg/t_Sorting_data.html)
* [Choosing a sort key](https://docs.aws.amazon.com/redshift/latest/dg/c_best-practices-sort-key.html)
* [Automatic table optimization](https://docs.aws.amazon.com/redshift/latest/dg/t_Creating_tables.html)

This is great if you notice that the sort key you're using isn't actually doing
much for the analyzer. While there are [auto sort keys](https://docs.aws.amazon.com/redshift/latest/dg/t_Creating_tables.html#ato-enabling),
if you're defining your own you can instead roll an `ALTER SORT KEY` to better refine your selection over time.

