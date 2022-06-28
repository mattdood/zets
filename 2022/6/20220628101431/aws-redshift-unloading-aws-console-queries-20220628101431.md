---
path: '/2022/6/aws-redshift-unloading-aws-console-queries-20220628101431'
title: 'aws redshift unloading aws console queries'
date: '20220628101431'
category: 'databases'
tags: ['aws', 'redshift', 's3', 'unload']
---

# aws redshift unloading aws console queries
When running queries in the AWS Redshift console often the result sizes are a bit
larger than the maximum returned limit that the browser supports.

AWS suggests wrapping the query in an `UNLOAD` operation to allow for all the
data to be returned. This can be a little tedious if you haven't worked with these
operations before, as they default to a pretty large number of files and become
difficult to work with rather quickly.

## General guidance
* All single quotes in your query should be [escaped](https://stackoverflow.com/a/48000345/12387496)
using a second single quote
    * Example: `'SOMETHING'` -> `''SOMETHING''` where each quote is a single quote (`'`)
    * **Note:** Redshift treats all double quotes (`"`) as a column name
* Keeping `PARALLEL OFF` will write to a single file (so long as it is below 6.25 GB in size)
    * This also respects an `ORDER BY` clause in the query
* If using this unloaded data for [Redshift Spectrum queries](https://docs.aws.amazon.com/redshift/latest/dg/c-getting-started-using-spectrum.html)
be sure to note the allowed data types of an [external table](https://docs.aws.amazon.com/redshift/latest/dg/r_CREATE_EXTERNAL_TABLE.html)
during your [external schema](https://docs.aws.amazon.com/redshift/latest/dg/r_CREATE_EXTERNAL_SCHEMA.html) creation

### A template to use for `UNLOAD` operations
Note that this will create a CSV file with the unloaded data, though the filename
will have a suffix `file-name.csv000` and will need to be renamed.

This isn't avoidable at the time of writing, so it will need to be renamed either
after downloading or while inside the S3 bucket with a rename operation.

```sql
UNLOAD ('
    <my query here>
')
TO 's3://my-bucket-name/folder/file-name.csv'
IAM_ROLE 'arn:aws:iam::12345678910:role/role-name-here'
NULL AS 'null'  -- set null values
HEADER  -- include column headers
MAXFILESIZE 6.2 GB  -- default max size, may change in the future
PARALLEL OFF  -- writes to 1 file, not multiple
ALLOWOVERWRITE  -- overwrite file between executions
GZIP  -- compress the file
CSV  -- file type
;
```

### Example `UNLOAD` operation
Below is an example query with an escaped singlequotes name.

```sql
UNLOAD ('
    SELECT
        *
    FROM
        people.customers c
    WHERE
        c.name ILIKE ''%smith''
    ORDER BY
        c.name DESC
')
TO 's3://my-bucket-name/folder/customers-by-name.csv'
IAM_ROLE 'arn:aws:iam::12345678910:role/role-name-here'
NULL AS 'null'  -- set null values
HEADER  -- include column headers
MAXFILESIZE 6.2 GB  -- default max size, may change in the future
PARALLEL OFF  -- writes to 1 file, not multiple
ALLOWOVERWRITE  -- overwrite file between executions
GZIP  -- compress the file
CSV  -- file type
;
```

