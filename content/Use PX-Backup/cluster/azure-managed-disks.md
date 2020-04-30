---
title: Add a cluster
description: 
keywords: 
weight: 3
hidesections: true
disableprevnext: true
---

## Azure with managed disks

<!-- AKS starts at 28:34 -->

add the cluster to PX-Backup
    In PX-Backup, Select **Add Cluster**
    From this page, enter the cluster details
        Name the cluster
        Retrieve the Kubeconfig from your cluster and paste it in the **Kubeconfig** text frame
        Select the **Others** radio button from the **Kubernetes Service** 
        from the **Cloud Account** dropdown, select the cloud account you previously created.
        Select the **Submit** button

Set environment variables on your cluster for Stork containing your Azure tenant ID, client ID, and client secret:

```text
kubectl create secret generic -n kube-system px-azure --from-literal=AZURE_TENANT_ID=<tenant> \
                                                      --from-literal=AZURE_CLIENT_ID=<appId> \
                                                      --from-literal=AZURE_CLIENT_SECRET=<password>
```

