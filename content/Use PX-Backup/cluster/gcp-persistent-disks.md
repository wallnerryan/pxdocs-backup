---
title: GCP with persistent disks
description: 
keywords: 
weight: 3
hidesections: true
disableprevnext: true
---

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
