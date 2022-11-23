---
path: '/2022/11/aws-redshift-lock-query-types-20221123150403'
title: 'aws redshift lock query types'
date: '20221123150403'
category: 'databases'
tags: ['redshift', 'lock waits']
---

# aws redshift lock query types
Detecting and releasing locks in Redshift is an important thing to consider
when working with large amounts of data.

In some cases you may encounter exclusive locking for things like `ALTER TABLE`
statements that block all other queries/locking attempts.

**References:**
* [How do I detect and release locks in Amazon Redshift](https://aws.amazon.com/premiumsupport/knowledge-center/prevent-locks-blocking-queries-redshift/)

However, for most Redshift queries we have 2 access types that we care about (from the Redshift documentation):
* `AccessShareLock`: Acquired during UNLOAD, SELECT, UPDATE, or DELETE operations.
AccessShareLock blocks only AccessExclusiveLock attempts. AccessShareLock doesn't
block other sessions that are trying to read or write on the table.
* `ShareRowExclusiveLock`: Acquired during COPY, INSERT, UPDATE, or DELETE operations.
ShareRowExclusiveLock blocks AccessExclusiveLock and other ShareRowExclusiveLock
attempts, but doesn't block AccessShareLock attempts.

For things like `VACUUM` operations we're able to handle on-disk reorganization
in the background because we have an `AccessShareLock` that does not block read operations
or writes to the database.

