---
title: RabbitMQ
description: 
keywords: 
weight: 4
hidesections: true
disableprevnext: true
---

This page provides instructions for users on how to use pre and post backups rules with PX-Backup to achieve application-consistent backups for RabbitMQ in production.


## Installation

### Prerequisites

{{% content "shared/common-info.md" %}}

{{<info>}}
**NOTE:** 
{{</info>}}

### Create rules for RabbitMQ

#### Create a pre-exec backup rule for RabbitMQ



{{<info>}}
**NOTE:** 
{{</info>}}



1. Navigate to **Settings** → **Rules** → **Add New**.
2. Add a name for your Rule.
3. Add the following app label:

	```text
	TODO
	```

4. Add the following action:

	```text
	TODO
	```

    IMG

#### Create a post-exec backup rule for RabbitMQ


{{<info>}}
**NOTE:** 
{{</info>}}

1. Navigate to **Settings** → **Rules** → **Add New**.
2. Add a name for your Rule.
3. Add the following app label:

	```text
	TODO
	```

4. Add the following action:

	```text
	TODO
	```

	IMG

### Use the rules during backup of RabbitMQ

During the backup creation process, select the rules in the **pre-exec** and **post-exec** drop downs:

IMG

Once you've filled out the backup form, click **Create**

## Demo

Watch this short demo of the above information.

{{< youtube  1RzFlmSMU-I >}}
