---
title: Configure cloud credentials
description: 
keywords: 
weight: 1
hidesections: true
disableprevnext: true
scrollspy-container: false
type: common-landing
---

Credentials allow PX-Backup to authenticate with clusters for the purpose of taking backups and restoring to them, as well as with backup locations where backup objects are stored. 

1. Generate a key with your GCP or AWS provider. PX-Central uses this key to authenticate with your cloud provider and store and retrieve backup images from your cloud storage buckets. 

2. From the home page, select **Settings**, **Cloud Settings** to open the cloud settings page.

    ![cloud settings](/img/cloud-settings.png)

3. Under the **Cloud Accounts** section, select **Add New**.

    ![add new cloud account](/img/add-new.png)

4. Choose the appropriate cloud provider, and populate the fields with your key information:

    * **Account Name**: specify the name with which this account will show in PX-Central
    * **For AWS**:

        * **Public Key**: the public key credentials you generated on AWS in step 1
        * **Secret Key**: the secret key credentials you generated in AWS in step 1
    
    ![populate cloud fields](/img/add-cloud-account.png)