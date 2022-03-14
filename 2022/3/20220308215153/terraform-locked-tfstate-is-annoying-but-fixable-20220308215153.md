---
path: '/2022/3/terraform-locked-tfstate-is-annoying-but-fixable-20220308215153'
title: 'terraform locked tfstate is annoying but fixable'
date: '20220308215153'
category: 'terraform'
tags: ['terraform', 'aws']
---

# terraform locked tfstate is annoying but fixable
When deploying some personal project resources I came upon a Terraform lock state
error. This was my own fault, I had `Ctrl+Z`'d my way out of a process and left
the `.tfstate` file locked up.

[Fortunately, I found this blog post discussing the issue](https://devcoops.com/how-to-fix-terraform-error-acquiring-state-lock/).
It was able to resolve my problem, though I had to kill the PID of the process.

## Solution
For safekeeping, I'll be keeping the solution here as well.

The error:
```
Acquiring state lock. This may take a few moments...
╷
│ Error: Error acquiring the state lock
│
│ Error message: ConditionalCheckFailedException: The conditional request failed
│ Lock Info:
│   ID:        c2024f2b-b615-05bf-e516-e49ed2852087
│   Path:      <...>
│   Operation: OperationTypePlan
│   Who:       <...>
│   Version:   1.0.2
│   Created:   2021-07-28 14:54:32.498842 +0000 UTC
│   Info:
│
│
│ Terraform acquires a state lock to protect the state from being written
│ by multiple users at the same time. Please resolve the issue above and try
│ again. For most commands, you can disable locking with the "-lock=false"
│ flag, but this is not recommended.
```

1. Attempt to unlock the process with the unlock command. Rerun your failing command after.
```
terraform force-unlock c2024f2b-b615-05bf-e516-e49ed2852087
```

2. If that fails, attempt to unlock the command with `-force`. Rerun your failing command after.
```
terraform force-unlock -force c2024f2b-b615-05bf-e516-e49ed2852087
```

**Note:** This might fail too, I received an error stating we can't release local `.tfstate`.

3. Find the PID of your process, kill it, then rerun your failing command.
```
ps aux | grep terraform
kill -9 <process-id>
```

