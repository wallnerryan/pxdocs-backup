---
title: AWS
description: 
keywords: 
weight: 1
hidesections: true
disableprevnext: true
scrollspy-container: false
type: common-landing
series2: get-started
series2_weight: 2
---

Perform the following steps to add an AWS cloud account to PX-Backup:

1. In AWS, create an IAM role with the following permissions:

* `ec2:CreateSnapshot`
* `ec2:CreateSnapshots`
* `ec2:DeleteSnapshot`
* `ec2:DescribeSnapshots`

{{<info>}}
**NOTE:** When you try to create a backup using the specified cloud account, make sure either the bucket is already created, or the credentials include permission to create the bucket
{{</info>}}

2. Add the cloud account to PX-Backup:
    
    1. Add new credentials in PX-Backup, under cloud settings, add a new **Cloud Account**.
    2. Choose **AWS / S3 Compliant Object Store**
    3. Enter a descriptive account name
    4. In the **Public Key** field, add your S3 access key ID
    5. In the **Secret Key** field, add your S3 secret access key
    6. Select the **Add** button

    ![](/img/aws-credential.png)