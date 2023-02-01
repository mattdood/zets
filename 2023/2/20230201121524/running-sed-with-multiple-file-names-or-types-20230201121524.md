---
path: '/2023/2/running-sed-with-multiple-file-names-or-types-20230201121524'
title: 'running sed with multiple file names or types'
date: '20230201121524'
category: 'bash'
tags: ['linux', 'tip', 'sed', 'bash']
---

# running sed with multiple file names or types
When running `sed` if we have a replacement that is present across multiple files
we can add some `OR` clauses to our operation.

## Example sed call using multiple file types
In the below example we're using multiple available file types with our `sed`
call.

**NOTE:** The below command *will run*, this is **NOT** a dry run command.

```bash
find . -type f \( -name '*.<my file extension>' -o -name 'example.txt' -o -name 'other-example.tf' \) -readable -writable -exec sed -i 's/<search string>/<replace string>/g' {} \;
```

The key portion to pay attention to is:

```
-type f \( -name 'something.here' -o -name 'something-else.here' \)
```

Note that the spaces between our `-type f` and `-name` are very important, as
well as the trailing space before our delimeter.

