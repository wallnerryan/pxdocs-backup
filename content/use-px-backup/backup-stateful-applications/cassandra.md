---
title: Cassandra
description: 
keywords: 
weight: 4
hidesections: true
disableprevnext: true
---

This page provides instructions for users on how to use pre- and post- backups rules with PX-Backup to achieve application consistent backups for Cassandra in production.

## Background

Cassandra is resilient to node failures, However, Cassandra backups are still necessary to recover from following scenarios.

Unauthorized deletions
Major failure’s that require a rebuild your entire cluster
Corrupt data
Point in time rollbacks
Disk failure

Cassandra provides an internal snapshot mechanism to take backups with a tool called nodetool. This can be setup to provide incremental or full snapshot based backups of the data on the node. This tool will flush data from memtables to disk and create a hardlink to the SSTables file on the node.

However, disadvantages of this include the fact that nodetool must be run on each and every cassandra node and data is kept locally increasing the overall storage footprint. What we’re suggesting is to let Portworx backup the cassandra PVs at a block level and ultimately store them in a space efficient object storage target. Portworx allows you to combine techniques that are recommended by cassandra such as flushing data to disk with pre-- and post-- hooks into the application to give you Kubernetes-native and efficient backup of Cassandra data.

PX-Backup allows application owners to set up pre- and post- hook rules that will be applied before and or after a backup occurs. For cassandra, users may want to create a custom flush, compaction, or verify to ensure a healthy and consistent data set before and after a backup occurs. Rules can run on one or all pods associated with Cassandra which is often a requirement for nodetool commands. 

For more information on how to run Cassandra on Kubernetes, read [this article][1].

## Installation

### Prerequisites

{{% content "use-px-backup/backup-stateful-applications/shared/common-info.md" %}}

{{<info>}}
Cassandra pods must also be using the `app=cassandra` label.
{{</info>}}

### Create rules for Cassandra

#### Create a pre- backup rule for Cassandra

Create a rule that will run `nodetool flush` for our `newkeyspace` before our backup. This is essential as Portworx will take a snapshot of the backing volume before it places that data in the backup target.

1. Navigate to Settings → Rules → Add New.
2. Add a name for your Rule.
3. Add the app label

`app=cassandra`

4. Add the Action

`nodetool flush -- <your-cassandra-keyspace>;`

 ![](/img/cassandra-pre-rule.png)

#### Create a post- backup rule for Cassandra

A post-exec backup rule for Cassandra isn't as necessary as the pre-exec backup rule above, however, for completeness in production and to verify the keyspace is no corrupt after the backup occurs we will create a rule that runs `nodetool verify`. The verify command will verify (check data checksums for) one or more tables.

1. Navigate to Settings → Rules → Add New.
2. Add a name for your Rule.
3. Add the app label

`app=cassandra`

4. Add the Action

`nodetool verify -- <your-cassandra-keyspace>;`

 ![](/img/cassandra-post-rule.png)

### Use the rules during backup of Cassandra

To use the Cassandra pre- and post- backup rules, select them as your pre-exec rule and post-exec rule when filling out the backup from in the PX-Backup interface. An example of what this looks like is below.

 ![](/img/cassandra-use-rules.png)

 Then click **Create**

[1]: https://docs.portworx.com/portworx-install-with-kubernetes/application-install-with-kubernetes/cassandra/ "cassandra application install"
