---
title: MySQL
description: 
keywords: 
weight: 4
hidesections: true
disableprevnext: true
---

This page provides instructions for users on how to use pre- and post- backups rules with PX-Backup to achieve application consistent backups for MySQL in production.

## Background

Information managed by MySQL server is stored in a location called the [data directory][2]. Often, this data directory is located in the MySQL server filesystem at `/var/lib/mysql`. Within this location are the files and data that are vital for MySQL to persist information, and this is why it’s important to mount Kubernetes PersistentVolumeClaims (PVCs) to the data directory location that the MySQL image uses. In Kubernetes, the spec file volumeMount may look like this:

```yaml
        volumeMounts:
        - name: mysql-data
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-data
        persistentVolumeClaim:
          claimName: mysql-data
```

Within the data directory, MySQL stores schema, table, logs, configuration and database data that corresponds to system, performance, and client data. Mounting a PersistentVolume enables PX-Backup to snapshot and back up MySQL data when needed.

MySQL has a tool called mysqldump which works well for taking backups specific to MySQL. Since PX-Backup can provide abstracted backup and restore for a polyglot of data services, we can replicate the [best practices of mysqldump][3], such as flushing and locking logs and tables into PX-Backup’s pre- and post- backup rules. PX-Backup rules and backups can be used across multiple instances of MySQL and multiple types of clouds. This will ultimately simplify operations for devops teams for single or multi-cloud workflows.

For more information on how to run MySQL on Kubernetes, read [this article][1].

## Installation

### Prerequisites

{{% content "use-px-backup/backup-stateful-applications/shared/common-info.md" %}}

{{<info>}}
MySQL pods must also be using the `app=mysql` label.
{{</info>}}

### Create rules for MySQL

#### Create a pre- backup rule for Cassandra

Before a backup of MySQL occurs, it is recommended to flush certain data to disk so that the backup remains consistent. Database tables and logs are examples of data that should be flushed. It is also important in MySQL to lock the tables so no new I/O transactions attempt to add records during the backup, or MySQL may also become inconsistent. 

To accomplish this, we can implement a `FLUSH TABLES WITH READ LOCK` command in our pre-backup rule. This will perform the following operations:

[(`FLUSH TABLES WITH READ LOCK`)][4] - Closes all open tables and locks all tables for all databases with a global read lock. This is a very convenient way to get backups if you have a file system such as Veritas or ZFS that can take snapshots in time. Use `UNLOCK TABLES` to release the lock.

Since PX-Backup performs a snapshot of the persistent volume in Kubernetes, this will accomplish what we are looking for.

{{<info>}}
Note: Set this rule to run in the background, which requires a `WAIT_CMD` to allow the rule to execute and exit properly.
{{</info>}}

Create the following rule within the PX-Backup interface. You may need to modify the username and password depending on how MySQL is configured in your Kubernetes environment.

1. Navigate to **Settings** → **Rules** → **Add New**.
2. Add a name for your Rule.
3. Add the app label

`app=mysql`

4. Add the Action

```bash
mysql --user=root --password=$MYSQL_ROOT_PASSWORD -Bse 'FLUSH TABLES WITH READ LOCK;system ${WAIT_CMD};'
```

 ![](/img/mysql-pre-rule.png)

#### Create a post- backup rule for Cassandra

Since we made sure to flush and lock data from MySQL before our backup, we must make sure to `UNLOCK` the database from the global read lock. MySQL documentation tells us that this is because global locks are not implicitly unlocked after the `FLUSH TABLES WITH READ LOCK` operation. It also may be a good idea to `FLUSH LOGS`, which “Closes and reopens any log file to which the server is writing” and updates the sequence number of the log. This may be required if users need a clear distinction between logs before and after a backup occurs. Flushing logs is optional here but will add it to our post- backup rule for completeness.

{{<info>}}
Note: Post- backup rules are not allowed to run in the background, a WAIT_CMD is not needed.
{{</info>}}

Create the following rule within the PX-Backup interface. You may need to modify the username and password depending on how MySQL is configured in your Kubernetes environment.

1. Navigate to **Settings** → **Rules** → **Add New**.
2. Add a name for your Rule.
3. Add the app label

`app=mysql`

4. Add the Action

```bash
mysql --user=root --password=$MYSQL_ROOT_PASSWORD -Bse 'FLUSH LOGS; UNLOCK TABLES;'
```

 ![](/img/mysql-post-rule.png)

### Use the rules during backup of MySQL

To use the MySQL pre- and post- backup rules, select them as your **pre-exec** rule and **post-exec** rule when filling out the backup from in the PX-Backup interface. An example of what this looks like is below.

![](/img/mysql-use-rules.png)

 Then click **Create**

[1]: https://portworx.com/mysql-kubernetes/ "mysql kubernetes"
[2]: https://dev.mysql.com/doc/refman/8.0/en/data-directory.html "data directory"
[3]: https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_add-locks "best practices"
[4]: https://dev.mysql.com/doc/refman/8.0/en/flush.html#flush-tables-with-read-lock "FLUSH TABLES WITH READ LOCK"
[5]: https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-snapshots/snaps-3d/#step-1-create-rules "wait cmd"
[6]: https://dev.mysql.com/doc/refman/8.0/en/flush.html#flush-logs "flush logs"