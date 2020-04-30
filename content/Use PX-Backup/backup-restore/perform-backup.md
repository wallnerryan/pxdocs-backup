---
title: Create a backup
description: 
keywords: 
weight: 5
hidesections: true
disableprevnext: true
---

Once you’ve created any backup rules and schedule policies you want, you can use them to create a backup. 

1. From the PX-Central home page, select the **Backup** button for the cluster you want to back up:

    ![](/img/select-backup.png)

2. Select the namespace and any labels you want to back up:

    ![](/img/select-namespace-labels.png)

3. Select the **Backup** button:

    ![](/img/select-create-backup.png)

4. From the dialog box, specify the following:
    
    * **Backup name**: the name of the backup you want displayed in the PX-Backup UI
    * **Destination location**: which bucket you want to store your backups onto
    * **Schedule**: Run the backup immediately or choose a schedule rule to associate with this backup
    * **Pre-exec rule**: any rules you want to execute before the backup runs
    * **Post-exec rule**: any rules you want to execture after the backup runs
    * **Backup labels**: any labels you want to attach to the backup once it's created

    ![](/img/populate-backup-fields.png)


<!-- 
## Perform a namespace-level backup



## Perform an app-level backup -->

