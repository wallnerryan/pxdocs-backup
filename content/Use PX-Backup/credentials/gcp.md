---
title: GCP
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

Perform the following steps to add a GCP cloud account to PX-Backup:

1. In GCP, create a **Compute Engine default** service account for use with your cluster. Modify the service account, adding **Read Write** access for each API. Save the JSON key for this service account for future reference.

2. Add the cloud account to PX-Backup:

    1. Add new credentials in PX-Backup, under cloud settings, add a new **Cloud Account**.
    2. Choose **Google Cloud**
    3. Create a descriptive account name
    4. add the JSON key for the service account associated with your GKE cluster
    5. Select the **Add** button

    ![](/img/gcp-account-add.png)