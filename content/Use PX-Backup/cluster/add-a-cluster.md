---
title: Add a cluster
description: 
keywords: 
weight: 3
hidesections: true
disableprevnext: true
---

Once you’ve installed PX-Backup, you’re ready to add any clusters you’d like to back up and restore to. How you prepare your cluster differs based on its environment. 

## Portworx clusters

If your cluster is running on Portworx, you don't need to do anything. Portworx includes Stork, allowing PX-Backup to take backups and restore them onto your cluster with no additional configuration. 
<!-- not so sure about this. True? -->

## AWS with EBS

Create an IAM role with the following permissions:

* `ec2:CreateSnapshot`
* `ec2:CreateSnapshots`
* `ec2:DeleteSnapshot`
* `ec2:DescribeSnapshots`

<!-- this may need to be moved to credentials creation topic -->
{{<info>}}
**NOTE:** When you try to create a backup using the specified cloud account, make sure either the bucket is already created, or the credentials include permission to create the bucket
{{</info>}}

## Azure with managed disks

Azure does not require you to add credentials for the cluster in PX-Central. Instead, set environment variables on your cluster for Stork containing your tenant ID, client ID, and client secret:

```text
kubectl create secret generic -n kube-system px-azure --from-literal=AZURE_TENANT_ID=<tenant> \
                                                      --from-literal=AZURE_CLIENT_ID=<appId> \
                                                      --from-literal=AZURE_CLIENT_SECRET=<password>
```

## GCP with persistent disks



### enable permissions

1. Create a kubernetes cluster on GCP
2. go to the security tab, under access scope, set access for each api
3. give it read/write access for compute engine

### add the cloud account

GCP

enter the JSON key. get it from IAM in GCP dashboard.
IAM > service accounts > actions > create key > choose key type JSON from the service account. once you do this, it generates the JSON. Copy that json and paste it into the JSON key field in the cloud account section of PX central. 

next, go to add cluster, get the kubeconfig: GKE dash > clusters > connect > run the command line access command > paste the kubectl config output into the cluster input on px-backup. 

The cluster now shows up and you can view everything from the application dashboard. 

create the cloud credential associated with the service account associated with the GKE cluster. 


clouds | using cloud volumes | 

GCP | 

1. If you’re using EKS or GKE, create cloud credentials.
2. Add your kubeconfig to PX-Central. ssh into your cluster and run the following command:
    
    ```text
    kubectl config view --flatten --minify
    ```