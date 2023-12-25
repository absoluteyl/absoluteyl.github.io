---
layout: single
title:  "[Terraform] Invalid legacy provider address"
date:  2023-12-25 13:54:00 +0800
categories: [terraform, aws]
---

## Problem

When I tried to run `terraform plan` or `terraform apply` command, I got following error message:

```bash
╷
│ Error: Invalid legacy provider address
│
│ This configuration or its associated state refers to the unqualified provider "aws".
│
│ You must complete the Terraform 0.13 upgrade process before upgrading to later versions.
╵
```

## Cause & Solution

After upgraded to 0.13, Terraform will use the new provider address format. Just run following command to upgrade the provider address format:

```bash
$ terraform state replace-provider registry.terraform.io/-/aws hashicorp/aws

Terraform will perform the following actions:

  ~ Updating provider:
    - registry.terraform.io/-/aws
    + registry.terraform.io/hashicorp/aws

Changing 5 resources:

  aws_ecr_repository.kkbook-service
  aws_iam_user_policy_attachment.gitlab-ci
  data.aws_iam_user.gitlab-ci
  aws_acm_certificate.star-kktv-me
  aws_ecr_repository.billing

Do you want to make these changes?
Only 'yes' will be accepted to continue.

Enter a value: yes

Successfully replaced provider for 5 resources.
```
