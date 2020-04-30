---
title: Add a cluster
description: 
keywords: 
weight: 3
hidesections: true
disableprevnext: true
---

Once you’ve installed PX-Backup, you’re ready to add any clusters you’d like to back up from and restore to. How you prepare your cluster differs based on its environment. If you're using a cloud-based kubernetes cluster, you must configure permissions on your cloud provider before adding it to PX-Backup.

## Portworx clusters

If your cluster is running on Portworx, you don't need to do anything. Portworx includes Stork, allowing PX-Backup to take backups and restore them onto your cluster with no additional configuration. 
<!-- not so sure about this. True? -->

## GCP with persistent disks

Modify the node security settings, Create a cluster role with compute engine read/write access. 

When creating your cluster on GKE:
    under **NODE POOLS** > **Node security**, select a service account; the Compute Engine default service account is sufficient.
    Under **Access scopes** within the **Node security** page, select the **Set access for each API** option. Under the **Compute Engine** dropdown, select **Read Write** 

Once the cluster has deployed:

Get the service account key associated with your cluster:
    get this from GCP dashboard: **IAM & Admin** > **IAM** > **Service Accounts** > **Actions...** > **Create Key** > JSON key type
    download the JSON key

add the cloud account to PX-Backup:
    Add new credentials in PX-Backup, under cloud settings, add a new **Cloud Account**.
    Choose **Google Cloud**
    Create a descriptive account name
    add the JSON key for the service account associated with your GKE cluster
    Select the **Add** button

add the cluster to PX-Backup
    Now that you've added the cloud account to PX-Backup, it can authenticate with your cluster on GCP and perform the operations necessary for backup tasks. 
    In PX-Backup, Select **Add Cluster**
    From this page, enter the cluster details
        Name the cluster
        Retrieve the Kubeconfig from your cluster and paste it in the **Kubeconfig** text frame
        Select the **GKE** radio button from the **Kubernetes Service** 
        from the **Cloud Account** dropdown, select the cloud account you previously created.
        Select the **Submit** button

{{<info>}}
**NOTE:** Your cluster must be running Stork 2.4 or higher. Copy and paste the command located under the **Cluster name** field if necessary.
{{</info>}}

## AWS with EBS

Create an IAM role with the following permissions:

* `ec2:CreateSnapshot`
* `ec2:CreateSnapshots`
* `ec2:DeleteSnapshot`
* `ec2:DescribeSnapshots`

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

<!-- this may need to be moved to credentials creation topic -->
{{<info>}}
**NOTE:** When you try to create a backup using the specified cloud account, make sure either the bucket is already created, or the credentials include permission to create the bucket
{{</info>}}

## Azure with managed disks

Set environment variables on your cluster for Stork containing your tenant ID, client ID, and client secret:

```text
kubectl create secret generic -n kube-system px-azure --from-literal=AZURE_TENANT_ID=<tenant> \
                                                      --from-literal=AZURE_CLIENT_ID=<appId> \
                                                      --from-literal=AZURE_CLIENT_SECRET=<password>
```





### add the cloud account

2. go to the security tab, under access scope, set access for each api

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