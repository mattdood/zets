---
path: '/2022/4/excel-iso-8601-timestamp-conversion-to-date-20220425132342'
title: 'excel iso 8601 timestamp conversion to date'
date: '20220425132342'
category: 'excel'
tags: ['datetime']
---

# excel iso 8601 timestamp conversion to date
Working in Excel is tedious and annoying when using date formats as a basis
for analysis.

Using a set of data with UTC time is practically unusable unless converting
it to a regular date object, which requires some Excel magic.

Date format for this formula with an example:
```
yyyy-MM-DDTHH:MM:SSZ
2020-01-01T12:00:00+00:00
```

Excel won't recognize the above as anything but a general value type, to convert
this we'll use the column next to the stored value.

```
=DATEVALUE(LEFT(<your-cell>, 10))+TIMEVALUE(MID(<your-cell>,12,8))
```

After this, format the column to be a date column with the required style.

