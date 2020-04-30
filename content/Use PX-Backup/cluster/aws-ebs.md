---
title: AWS with EBS
description: 
keywords: 
weight: 3
hidesections: true
disableprevnext: true
---

Create an IAM role with the following permissions:

* `ec2:CreateSnapshot`
* `ec2:CreateSnapshots`
* `ec2:DeleteSnapshot`
* `ec2:DescribeSnapshots`

<!-- this may need to be moved to credentials creation topic -->
{{<info>}}
**NOTE:** When you try to create a backup using the specified cloud account, make sure either the bucket is already created, or the credentials include permission to create the bucket
{{</info>}}

add the cloud account to PX-Backup:
    Add new credentials in PX-Backup, under cloud settings, add a new **Cloud Account**.
    Choose **AWS / S3 Compliant Object Store**
    Enter a descriptive account name
    In the **Public Key** field, add your S3 access key ID
    In the **Secret Key** field, add your S3 secret access key
    Select the **Add** button

add the cluster to PX-Backup
    Now that you've added the cloud account to PX-Backup, it can authenticate with your cluster on AWS and perform the operations necessary for backup tasks. 
    In PX-Backup, Select **Add Cluster**
    From this page, enter the cluster details
        Name the cluster
        Retrieve the Kubeconfig from your cluster and paste it in the **Kubeconfig** text frame
        Select the **EKS** radio button from the **Kubernetes Service** 
        from the **Cloud Account** dropdown, select the cloud account you previously created.
        Select the **Submit** button

