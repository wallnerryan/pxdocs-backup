---
title: GKE
description:
keywords:
weight: 3
hidesections: true
disableprevnext: true
---

## Prerequisites

* You've added your GCP cloud account to PX-Backup. See the [GCP](/use-px-backup/credentials/gcp/) page for more details about how you can add an GCP account to PX-Backup.

* Your cluster must be running Stork 2.4 or higher. To install Stork on your Kubernetes cluster, copy and paste the command displayed below the **Cloud Account** radio group.

## Add the cluster to PX-Backup

1. From the home page, select **Add Cluster**:

    ![Add cluster](/img/add-cluster.png)

2. On the **Add Kubernetes Cluster** page, enter the cluster details:
    * The name of the cluster
    * Retrieve the Kubeconfig from your cluster and paste it in the **Kubeconfig** text frame, or select the **Browse** button to upload it from a file.
    * Select the **GKE** radio button from the **Kubernetes Service** radio group
    * From the **Cloud Account** dropdown, select your GCP cloud account.
    * Select the **Submit** button

    ![Enter the cluster details](/img/enter-gcp-gke-cluster-details.png)

3. Select the **Submit** button


<!-- Modify the node security settings, Create a cluster role with compute engine read/write access.

When creating your cluster on GKE:

1. Under **NODE POOLS** > **Node security**, select a service account; the Compute Engine default service account is sufficient.
2. Under **Access scopes** within the **Node security** page, select the **Set access for each API** option. Under the **Compute Engine** dropdown, select **Read Write**

Once the cluster has deployed:
2. Get the service account key associated with your cluster:
    1. get this from GCP dashboard: **IAM & Admin** > **IAM** > **Service Accounts** > **Actions...** > **Create Key** > JSON key type
    download the JSON key
    -->
