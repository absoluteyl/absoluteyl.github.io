---
layout: single
title:  "[Terraform] Error acquiring the state lock"
date:  2023-12-25 14:03:00 +0800
categories: [terraform, aws]
---

## Problem

Sometimes when I suspend a `terraform plan` or `terraform apply` action, then run it again, I got following error message:

```bash
│ Error: Error acquiring the state lock
│
│ Error message: ConditionalCheckFailedException: The conditional request failed
│ Lock Info:
│   ID:        <state_lock_id>
│   Path:      <path_to_the_state_file>
│   Operation: OperationTypeApply
│   Who:       <who_performed_last_action>
│   Version:   1.3.4
│   Created:   2023-12-24 09:21:26.126685 +0000 UTC
│   Info:
│
│
│ Terraform acquires a state lock to protect the state from being written
│ by multiple users at the same time. Please resolve the issue above and try
│ again. For most commands, you can disable locking with the "-lock=false"
│ flag, but this is not recommended.
╵
```

## Solution

You should probably as if anyone else are performing another action to the same state file. But if you are sure that no one is using the state file, you can remove the state lock by running following command:

```bash
terraform force-unlock <state_lock_id>
```
