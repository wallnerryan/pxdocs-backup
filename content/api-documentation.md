---
title: PX-Backup API Documentation
language_tabs:
  - shell: curl
language_clients:
  - shell: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2
---

You can use the PX-Backup API to create, schedule, and restore backups.

## Create creates a new backup object

<a id="opIdBackup_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/backup \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/backup`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "pre_exec_rule": "string",
  "post_exec_rule": "string"
}
```

<h4 id="create-creates-a-new-backup-object-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BackupCreateRequest](#schemabackupcreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-a-new-backup-object-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupCreateResponse](#schemabackupcreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update given backup details

<a id="opIdBackup_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/backup \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/backup`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  }
}
```

<h4 id="update-given-backup-details-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BackupUpdateRequest](#schemabackupupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-given-backup-details-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupUpdateResponse](#schemabackupupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of objects

<a id="opIdBackup_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/backup/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/backup/{org_id}`

<h4 id="enumerate-returns-a-list-of-objects-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|Organization id|
|enumerate_options.page_size|query|string(int64)|false|max objects to fetch.|
|enumerate_options.continuation_token|query|string|false|continuation token.|
|enumerate_options.time_range.start_time|query|string(date-time)|false|none|
|enumerate_options.time_range.end_time|query|string(date-time)|false|none|
|enumerate_options.name_filter|query|string|false|Filter to use for name of objects. Any object that contains the filter|
|enumerate_options.cluster_name_filter|query|string|false|Filter to use for cluster name of objects. Any object that contains the|

#### Detailed descriptions

**enumerate_options.name_filter**: Filter to use for name of objects. Any object that contains the filter
will be returned.

**enumerate_options.cluster_name_filter**: Filter to use for cluster name of objects. Any object that contains the
filter will be returned.

#### Example response

_200 Response_

```json
{
  "backups": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "backup_info": {
        "backup_location": "string",
        "cluster": "string",
        "namespaces": [
          "string"
        ],
        "label_selectors": {
          "property1": "string",
          "property2": "string"
        },
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "resources": [
          {
            "name": "string",
            "namespace": "string",
            "group": "string",
            "kind": "string",
            "version": "string"
          }
        ],
        "volumes": [
          {
            "name": "string",
            "namespace": "string",
            "pvc": "string",
            "backup_id": "string",
            "status": {
              "status": "Invalid",
              "reason": "string"
            },
            "driver_name": "string",
            "zones": [
              "string"
            ],
            "options": {
              "property1": "string",
              "property2": "string"
            }
          }
        ],
        "backup_path": "string",
        "stage": "Invalid",
        "pre_exec_rule": "string",
        "post_exec_rule": "string",
        "backup_schedule": {
          "uid": "string",
          "name": "string"
        },
        "cr_name": "string"
      }
    }
  ],
  "continuation_token": "string"
}
```

<h4 id="enumerate-returns-a-list-of-objects-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupEnumerateResponse](#schemabackupenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detail information about a specified object

<a id="opIdBackup_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/backup/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/backup/{org_id}/{name}`

<h4 id="inspect-returns-detail-information-about-a-specified-object-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "backup": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "backup_info": {
      "backup_location": "string",
      "cluster": "string",
      "namespaces": [
        "string"
      ],
      "label_selectors": {
        "property1": "string",
        "property2": "string"
      },
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "resources": [
        {
          "name": "string",
          "namespace": "string",
          "group": "string",
          "kind": "string",
          "version": "string"
        }
      ],
      "volumes": [
        {
          "name": "string",
          "namespace": "string",
          "pvc": "string",
          "backup_id": "string",
          "status": {
            "status": "Invalid",
            "reason": "string"
          },
          "driver_name": "string",
          "zones": [
            "string"
          ],
          "options": {
            "property1": "string",
            "property2": "string"
          }
        }
      ],
      "backup_path": "string",
      "stage": "Invalid",
      "pre_exec_rule": "string",
      "post_exec_rule": "string",
      "backup_schedule": {
        "uid": "string",
        "name": "string"
      },
      "cr_name": "string"
    }
  }
}
```

<h4 id="inspect-returns-detail-information-about-a-specified-object-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupInspectResponse](#schemabackupinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete triggers delete of a backup

<a id="opIdBackup_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/backup/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/backup/{org_id}/{name}`

<h4 id="delete-triggers-delete-of-a-backup-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-triggers-delete-of-a-backup-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupDeleteResponse](#schemabackupdeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-backuplocation">BackupLocation</h1>

## Create creates new backup location

<a id="opIdBackupLocation_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/backuplocation \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/backuplocation`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_location": {
    "type": "Invalid",
    "path": "string",
    "encryption_key": "string",
    "cloud_credential": "string",
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "delete_backups": true,
    "s3_config": {
      "endpoint": "string",
      "region": "string",
      "disable_ssl": true,
      "disable_path_style": true
    }
  }
}
```

<h4 id="create-creates-new-backup-location-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BackupLocationCreateRequest](#schemabackuplocationcreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-new-backup-location-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupLocationCreateResponse](#schemabackuplocationcreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update given backup location details

<a id="opIdBackupLocation_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/backuplocation \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/backuplocation`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_location": {
    "type": "Invalid",
    "path": "string",
    "encryption_key": "string",
    "cloud_credential": "string",
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "delete_backups": true,
    "s3_config": {
      "endpoint": "string",
      "region": "string",
      "disable_ssl": true,
      "disable_path_style": true
    }
  }
}
```

<h4 id="update-given-backup-location-details-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BackupLocationUpdateRequest](#schemabackuplocationupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-given-backup-location-details-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupLocationUpdateResponse](#schemabackuplocationupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of backup locations

<a id="opIdBackupLocation_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/backuplocation/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/backuplocation/{org_id}`

<h4 id="enumerate-returns-a-list-of-backup-locations-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "backup_locations": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "backup_location_info": {
        "type": "Invalid",
        "path": "string",
        "encryption_key": "string",
        "cloud_credential": "string",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "delete_backups": true,
        "s3_config": {
          "endpoint": "string",
          "region": "string",
          "disable_ssl": true,
          "disable_path_style": true
        }
      }
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-backup-locations-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupLocationEnumerateResponse](#schemabackuplocationenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detailed information about a specified backup location

<a id="opIdBackupLocation_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/backuplocation/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/backuplocation/{org_id}/{name}`

<h4 id="inspect-returns-detailed-information-about-a-specified-backup-location-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "backup_location": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "backup_location_info": {
      "type": "Invalid",
      "path": "string",
      "encryption_key": "string",
      "cloud_credential": "string",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "delete_backups": true,
      "s3_config": {
        "endpoint": "string",
        "region": "string",
        "disable_ssl": true,
        "disable_path_style": true
      }
    }
  }
}
```

<h4 id="inspect-returns-detailed-information-about-a-specified-backup-location-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupLocationInspectResponse](#schemabackuplocationinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete removes a backup location

<a id="opIdBackupLocation_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/backuplocation/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/backuplocation/{org_id}/{name}`

<h4 id="delete-removes-a-backup-location-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|
|delete_backups|query|boolean(boolean)|false|delete_backups indicates whether the cloud backup files need to|

#### Detailed descriptions

**delete_backups**: delete_backups indicates whether the cloud backup files need to
be deleted or retained.

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-removes-a-backup-location-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupLocationDeleteResponse](#schemabackuplocationdeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-backupschedule">BackupSchedule</h1>

## Create creates new backup schedule

<a id="opIdBackupSchedule_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/backupschedule \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/backupschedule`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": "string",
  "reclaim_policy": "Invalid",
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "pre_exec_rule": "string",
  "post_exec_rule": "string"
}
```

<h4 id="create-creates-new-backup-schedule-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BackupScheduleCreateRequest](#schemabackupschedulecreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-new-backup-schedule-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupScheduleCreateResponse](#schemabackupschedulecreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update updates a backup schedule

<a id="opIdBackupSchedule_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/backupschedule \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/backupschedule`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": "string",
  "reclaim_policy": "Invalid",
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "pre_exec_rule": "string",
  "post_exec_rule": "string",
  "suspend": true
}
```

<h4 id="update-updates-a-backup-schedule-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BackupScheduleUpdateRequest](#schemabackupscheduleupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-updates-a-backup-schedule-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupScheduleUpdateResponse](#schemabackupscheduleupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of backup schedule

<a id="opIdBackupSchedule_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/backupschedule/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/backupschedule/{org_id}`

<h4 id="enumerate-returns-a-list-of-backup-schedule-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "backup_schedules": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "backup_schedule_info": {
        "schedule_policy": "string",
        "suspend": true,
        "reclaim_policy": "Invalid",
        "backup_status": {
          "property1": {
            "status": [
              {
                "backup_name": "string",
                "create_time": "2020-04-29T05:40:19Z",
                "finish_time": "2020-04-29T05:40:19Z",
                "status": "Invalid"
              }
            ]
          },
          "property2": {
            "status": [
              {
                "backup_name": "string",
                "create_time": "2020-04-29T05:40:19Z",
                "finish_time": "2020-04-29T05:40:19Z",
                "status": "Invalid"
              }
            ]
          }
        },
        "backup_location": "string",
        "cluster": "string",
        "namespaces": [
          "string"
        ],
        "label_selectors": {
          "property1": "string",
          "property2": "string"
        },
        "pre_exec_rule": "string",
        "post_exec_rule": "string",
        "delete_backups": true,
        "status": {
          "backup_name": "string",
          "create_time": "2020-04-29T05:40:19Z",
          "finish_time": "2020-04-29T05:40:19Z",
          "status": "Invalid"
        },
        "suspended_by": {
          "source": "Invalid"
        }
      }
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-backup-schedule-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupScheduleEnumerateResponse](#schemabackupscheduleenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detail information about a specified backup schedule

<a id="opIdBackupSchedule_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/backupschedule/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/backupschedule/{org_id}/{name}`

<h4 id="inspect-returns-detail-information-about-a-specified-backup-schedule-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "backup_schedule": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "backup_schedule_info": {
      "schedule_policy": "string",
      "suspend": true,
      "reclaim_policy": "Invalid",
      "backup_status": {
        "property1": {
          "status": [
            {
              "backup_name": "string",
              "create_time": "2020-04-29T05:40:19Z",
              "finish_time": "2020-04-29T05:40:19Z",
              "status": "Invalid"
            }
          ]
        },
        "property2": {
          "status": [
            {
              "backup_name": "string",
              "create_time": "2020-04-29T05:40:19Z",
              "finish_time": "2020-04-29T05:40:19Z",
              "status": "Invalid"
            }
          ]
        }
      },
      "backup_location": "string",
      "cluster": "string",
      "namespaces": [
        "string"
      ],
      "label_selectors": {
        "property1": "string",
        "property2": "string"
      },
      "pre_exec_rule": "string",
      "post_exec_rule": "string",
      "delete_backups": true,
      "status": {
        "backup_name": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "finish_time": "2020-04-29T05:40:19Z",
        "status": "Invalid"
      },
      "suspended_by": {
        "source": "Invalid"
      }
    }
  }
}
```

<h4 id="inspect-returns-detail-information-about-a-specified-backup-schedule-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupScheduleInspectResponse](#schemabackupscheduleinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete removes a backup schedule

<a id="opIdBackupSchedule_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/backupschedule/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/backupschedule/{org_id}/{name}`

<h4 id="delete-removes-a-backup-schedule-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|
|delete_backups|query|boolean(boolean)|false|delete_backups indicates whether the cloud backup files need to|

#### Detailed descriptions

**delete_backups**: delete_backups indicates whether the cloud backup files need to
be deleted or retained.

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-removes-a-backup-schedule-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[BackupScheduleDeleteResponse](#schemabackupscheduledeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-cloudcredential">CloudCredential</h1>

## Create creates new cloud credential

<a id="opIdCloudCredential_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/cloudcredential \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/cloudcredential`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "cloud_credential": {
    "type": "Invalid",
    "aws_config": {
      "access_key": "string",
      "secret_key": "string"
    },
    "azure_config": {
      "account_name": "string",
      "account_key": "string",
      "client_secret": "string",
      "client_id": "string",
      "tenant_id": "string",
      "subscription_id": "string"
    },
    "google_config": {
      "project_id": "string",
      "json_key": "string"
    }
  }
}
```

<h4 id="create-creates-new-cloud-credential-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[CloudCredentialCreateRequest](#schemacloudcredentialcreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-new-cloud-credential-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[CloudCredentialCreateResponse](#schemacloudcredentialcreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update given cloud credential details

<a id="opIdCloudCredential_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/cloudcredential \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/cloudcredential`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "cloud_credential": {
    "type": "Invalid",
    "aws_config": {
      "access_key": "string",
      "secret_key": "string"
    },
    "azure_config": {
      "account_name": "string",
      "account_key": "string",
      "client_secret": "string",
      "client_id": "string",
      "tenant_id": "string",
      "subscription_id": "string"
    },
    "google_config": {
      "project_id": "string",
      "json_key": "string"
    }
  }
}
```

<h4 id="update-given-cloud-credential-details-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[CloudCredentialUpdateRequest](#schemacloudcredentialupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-given-cloud-credential-details-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[CloudCredentialUpdateResponse](#schemacloudcredentialupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of cloud credentials

<a id="opIdCloudCredential_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/cloudcredential/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/cloudcredential/{org_id}`

<h4 id="enumerate-returns-a-list-of-cloud-credentials-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|include_secrets|query|boolean(boolean)|false|none|

#### Example response

_200 Response_

```json
{
  "cloud_credentials": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "cloud_credential_info": {
        "type": "Invalid",
        "aws_config": {
          "access_key": "string",
          "secret_key": "string"
        },
        "azure_config": {
          "account_name": "string",
          "account_key": "string",
          "client_secret": "string",
          "client_id": "string",
          "tenant_id": "string",
          "subscription_id": "string"
        },
        "google_config": {
          "project_id": "string",
          "json_key": "string"
        }
      }
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-cloud-credentials-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[CloudCredentialEnumerateResponse](#schemacloudcredentialenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detailed information about the specified cloud credential

<a id="opIdCloudCredential_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/cloudcredential/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/cloudcredential/{org_id}/{name}`

<h4 id="inspect-returns-detailed-information-about-the-specified-cloud-credential-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|
|include_secrets|query|boolean(boolean)|false|none|

#### Example response

_200 Response_

```json
{
  "cloud_credential": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "cloud_credential_info": {
      "type": "Invalid",
      "aws_config": {
        "access_key": "string",
        "secret_key": "string"
      },
      "azure_config": {
        "account_name": "string",
        "account_key": "string",
        "client_secret": "string",
        "client_id": "string",
        "tenant_id": "string",
        "subscription_id": "string"
      },
      "google_config": {
        "project_id": "string",
        "json_key": "string"
      }
    }
  }
}
```

<h4 id="inspect-returns-detailed-information-about-the-specified-cloud-credential-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[CloudCredentialInspectResponse](#schemacloudcredentialinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete removes a cloud credential

<a id="opIdCloudCredential_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/cloudcredential/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/cloudcredential/{org_id}/{name}`

<h4 id="delete-removes-a-cloud-credential-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-removes-a-cloud-credential-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[CloudCredentialDeleteResponse](#schemacloudcredentialdeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-cluster">Cluster</h1>

## Create creates a new cluster

<a id="opIdCluster_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/cluster \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/cluster`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "px_config": {
    "access_token": "string"
  },
  "kubeconfig": "string",
  "cloud_credential": "string"
}
```

<h4 id="create-creates-a-new-cluster-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ClusterCreateRequest](#schemaclustercreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-a-new-cluster-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[ClusterCreateResponse](#schemaclustercreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update given cluster details

<a id="opIdCluster_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/cluster \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/cluster`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "px_config": {
    "access_token": "string"
  },
  "kubeconfig": "string",
  "cloud_credential": "string"
}
```

<h4 id="update-given-cluster-details-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[ClusterUpdateRequest](#schemaclusterupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-given-cluster-details-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[ClusterUpdateResponse](#schemaclusterupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of clusters

<a id="opIdCluster_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/cluster/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/cluster/{org_id}`

<h4 id="enumerate-returns-a-list-of-clusters-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "clusters": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "clusterInfo": {
        "px_config": {
          "access_token": "string"
        },
        "kubeconfig": "string",
        "cloud_credential": "string",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "delete_backups": true,
        "delete_restores": true
      }
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-clusters-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[ClusterEnumerateResponse](#schemaclusterenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detail information about a specified cluster

<a id="opIdCluster_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/cluster/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/cluster/{org_id}/{name}`

<h4 id="inspect-returns-detail-information-about-a-specified-cluster-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "cluster": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "clusterInfo": {
      "px_config": {
        "access_token": "string"
      },
      "kubeconfig": "string",
      "cloud_credential": "string",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "delete_backups": true,
      "delete_restores": true
    }
  }
}
```

<h4 id="inspect-returns-detail-information-about-a-specified-cluster-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[ClusterInspectResponse](#schemaclusterinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete removes a cluster

<a id="opIdCluster_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/cluster/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/cluster/{org_id}/{name}`

<h4 id="delete-removes-a-cluster-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|
|delete_backups|query|boolean(boolean)|false|delete_backups indicates whether the backup related to cluster need to|
|delete_restores|query|boolean(boolean)|false|delete_restores indicates whether the restore related to cluster  need to|

#### Detailed descriptions

**delete_backups**: delete_backups indicates whether the backup related to cluster need to
be deleted or retained.

**delete_restores**: delete_restores indicates whether the restore related to cluster  need to
be deleted or retained.

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-removes-a-cluster-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[ClusterDeleteResponse](#schemaclusterdeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-health">Health</h1>

## Status checks the health of the server

<a id="opIdHealth_Status"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/health \
  -H 'Accept: application/json'

```

`GET /v1/health`

#### Example response

_200 Response_

```json
{}
```

<h4 id="status-checks-the-health-of-the-server-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[HealthStatusResponse](#schemahealthstatusresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-license">License</h1>

## Activate activate a new license

<a id="opIdLicense_Activate"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/license \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/license`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "activation_id": "string",
  "license_data": "string"
}
```

<h4 id="activate-activate-a-new-license-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[LicenseActivateRequest](#schemalicenseactivaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="activate-activate-a-new-license-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[LicenseActivateResponse](#schemalicenseactivateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of license for given cluster

<a id="opIdLicense_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/license/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/license/{org_id}`

<h4 id="enumerate-returns-a-list-of-license-for-given-cluster-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "response_info": [
    {
      "name": "string",
      "count": "string",
      "expires": "2020-04-29T05:40:19Z",
      "starts": "2020-04-29T05:40:19Z"
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-license-for-given-cluster-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[LicenseInspectResponse](#schemalicenseinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-organization">Organization</h1>

## Enumerate returns a list of organization object

<a id="opIdOrganization_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/organization \
  -H 'Accept: application/json'

```

`GET /v1/organization`

#### Example response

_200 Response_

```json
{
  "organizations": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      }
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-organization-object-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[OrganizationEnumerateResponse](#schemaorganizationenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Create creates new organization object in datastore

<a id="opIdOrganization_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/organization \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/organization`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  }
}
```

<h4 id="create-creates-new-organization-object-in-datastore-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[OrganizationCreateRequest](#schemaorganizationcreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-new-organization-object-in-datastore-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[OrganizationCreateResponse](#schemaorganizationcreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detailed information about specified organization object

<a id="opIdOrganization_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/organization/{name} \
  -H 'Accept: application/json'

```

`GET /v1/organization/{name}`

<h4 id="inspect-returns-detailed-information-about-specified-organization-object-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "organization": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    }
  }
}
```

<h4 id="inspect-returns-detailed-information-about-specified-organization-object-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[OrganizationInspectResponse](#schemaorganizationinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-restore">Restore</h1>

## Create creates new restore object in datastore
It will also trigger a restore operation on the target cluster

<a id="opIdRestore_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/restore \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/restore`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup": "string",
  "cluster": "string",
  "namespace_mapping": {
    "property1": "string",
    "property2": "string"
  },
  "replace_policy": "Invalid"
}
```

<h4 id="create-creates-new-restore-object-in-datastore
it-will-also-trigger-a-restore-operation-on-the-target-cluster-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[RestoreCreateRequest](#schemarestorecreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-new-restore-object-in-datastore
it-will-also-trigger-a-restore-operation-on-the-target-cluster-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RestoreCreateResponse](#schemarestorecreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update given restore details

<a id="opIdRestore_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/restore \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/restore`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  }
}
```

<h4 id="update-given-restore-details-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[RestoreUpdateRequest](#schemarestoreupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-given-restore-details-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RestoreUpdateResponse](#schemarestoreupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of restore objects

<a id="opIdRestore_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/restore/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/restore/{org_id}`

<h4 id="enumerate-returns-a-list-of-restore-objects-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|Organization id|
|enumerate_options.page_size|query|string(int64)|false|max objects to fetch.|
|enumerate_options.continuation_token|query|string|false|continuation token.|
|enumerate_options.time_range.start_time|query|string(date-time)|false|none|
|enumerate_options.time_range.end_time|query|string(date-time)|false|none|
|enumerate_options.name_filter|query|string|false|Filter to use for name of objects. Any object that contains the filter|
|enumerate_options.cluster_name_filter|query|string|false|Filter to use for cluster name of objects. Any object that contains the|

#### Detailed descriptions

**enumerate_options.name_filter**: Filter to use for name of objects. Any object that contains the filter
will be returned.

**enumerate_options.cluster_name_filter**: Filter to use for cluster name of objects. Any object that contains the
filter will be returned.

#### Example response

_200 Response_

```json
{
  "restores": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "restore_info": {
        "backup": "string",
        "backup_location": "string",
        "label_selectors": {
          "property1": "string",
          "property2": "string"
        },
        "namespace_mapping": {
          "property1": "string",
          "property2": "string"
        },
        "replace_policy": "Invalid",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "resources": [
          {
            "name": "string",
            "namespace": "string",
            "group": "string",
            "kind": "string",
            "version": "string",
            "status": {
              "status": "Invalid",
              "reason": "string"
            }
          }
        ],
        "volumes": [
          {
            "pvc": "string",
            "source_namespace": "string",
            "source_volume": "string",
            "restore_volume": "string",
            "status": {
              "status": "Invalid",
              "reason": "string"
            },
            "driver_name": "string",
            "zones": [
              "string"
            ],
            "options": {
              "property1": "string",
              "property2": "string"
            }
          }
        ],
        "cluster": "string"
      }
    }
  ],
  "continuation_token": "string"
}
```

<h4 id="enumerate-returns-a-list-of-restore-objects-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RestoreEnumerateResponse](#schemarestoreenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detailed information about specified restore object

<a id="opIdRestore_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/restore/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/restore/{org_id}/{name}`

<h4 id="inspect-returns-detailed-information-about-specified-restore-object-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "restore": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "restore_info": {
      "backup": "string",
      "backup_location": "string",
      "label_selectors": {
        "property1": "string",
        "property2": "string"
      },
      "namespace_mapping": {
        "property1": "string",
        "property2": "string"
      },
      "replace_policy": "Invalid",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "resources": [
        {
          "name": "string",
          "namespace": "string",
          "group": "string",
          "kind": "string",
          "version": "string",
          "status": {
            "status": "Invalid",
            "reason": "string"
          }
        }
      ],
      "volumes": [
        {
          "pvc": "string",
          "source_namespace": "string",
          "source_volume": "string",
          "restore_volume": "string",
          "status": {
            "status": "Invalid",
            "reason": "string"
          },
          "driver_name": "string",
          "zones": [
            "string"
          ],
          "options": {
            "property1": "string",
            "property2": "string"
          }
        }
      ],
      "cluster": "string"
    }
  }
}
```

<h4 id="inspect-returns-detailed-information-about-specified-restore-object-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RestoreInspectResponse](#schemarestoreinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete removes a restore object

<a id="opIdRestore_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/restore/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/restore/{org_id}/{name}`

<h4 id="delete-removes-a-restore-object-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-removes-a-restore-object-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RestoreDeleteResponse](#schemarestoredeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-rules">Rules</h1>

## Create creates new rule

<a id="opIdRules_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/rule \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/rule`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "rules_info": {
    "rules": [
      {
        "pod_selector": {
          "property1": "string",
          "property2": "string"
        },
        "actions": [
          {
            "background": true,
            "run_in_single_pod": true,
            "value": "string"
          }
        ]
      }
    ]
  }
}
```

<h4 id="create-creates-new-rule-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[RuleCreateRequest](#schemarulecreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-new-rule-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RuleCreateResponse](#schemarulecreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update given rule details

<a id="opIdRules_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/rule \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/rule`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "rules_info": {
    "rules": [
      {
        "pod_selector": {
          "property1": "string",
          "property2": "string"
        },
        "actions": [
          {
            "background": true,
            "run_in_single_pod": true,
            "value": "string"
          }
        ]
      }
    ]
  }
}
```

<h4 id="update-given-rule-details-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[RuleUpdateRequest](#schemaruleupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-given-rule-details-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RuleUpdateResponse](#schemaruleupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of rules

<a id="opIdRules_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/rule/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/rule/{org_id}`

<h4 id="enumerate-returns-a-list-of-rules-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "rules": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "rules_info": {
        "rules": [
          {
            "pod_selector": {
              "property1": "string",
              "property2": "string"
            },
            "actions": [
              {
                "background": true,
                "run_in_single_pod": true,
                "value": "string"
              }
            ]
          }
        ]
      }
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-rules-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RuleEnumerateResponse](#schemaruleenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detailed information about the specified rule

<a id="opIdRules_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/rule/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/rule/{org_id}/{name}`

<h4 id="inspect-returns-detailed-information-about-the-specified-rule-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "rule": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "rules_info": {
      "rules": [
        {
          "pod_selector": {
            "property1": "string",
            "property2": "string"
          },
          "actions": [
            {
              "background": true,
              "run_in_single_pod": true,
              "value": "string"
            }
          ]
        }
      ]
    }
  }
}
```

<h4 id="inspect-returns-detailed-information-about-the-specified-rule-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RuleInspectResponse](#schemaruleinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete removes rule from px-backup

<a id="opIdRules_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/rule/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/rule/{org_id}/{name}`

<h4 id="delete-removes-rule-from-px-backup-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-removes-rule-from-px-backup-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[RuleDeleteResponse](#schemaruledeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-schedulepolicy">SchedulePolicy</h1>

## Create creates new schedule policy.

<a id="opIdSchedulePolicy_Create"></a>

#### Code sample

```shell
# You can also use wget
curl -X POST /v1/schedulepolicy \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`POST /v1/schedulepolicy`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": {
    "interval": {
      "minutes": "string",
      "retain": "string"
    },
    "daily": {
      "time": "string",
      "retain": "string"
    },
    "weekly": {
      "day": "string",
      "time": "string",
      "retain": "string"
    },
    "monthly": {
      "date": "string",
      "time": "string",
      "retain": "string"
    },
    "backup_schedule": [
      "string"
    ]
  }
}
```

<h4 id="create-creates-new-schedule-policy.-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SchedulePolicyCreateRequest](#schemaschedulepolicycreaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="create-creates-new-schedule-policy.-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[SchedulePolicyCreateResponse](#schemaschedulepolicycreateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Update given schedule policy details

<a id="opIdSchedulePolicy_Update"></a>

#### Code sample

```shell
# You can also use wget
curl -X PUT /v1/schedulepolicy \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json'

```

`PUT /v1/schedulepolicy`

_Body parameter_

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": {
    "interval": {
      "minutes": "string",
      "retain": "string"
    },
    "daily": {
      "time": "string",
      "retain": "string"
    },
    "weekly": {
      "day": "string",
      "time": "string",
      "retain": "string"
    },
    "monthly": {
      "date": "string",
      "time": "string",
      "retain": "string"
    },
    "backup_schedule": [
      "string"
    ]
  }
}
```

<h4 id="update-given-schedule-policy-details-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[SchedulePolicyUpdateRequest](#schemaschedulepolicyupdaterequest)|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="update-given-schedule-policy-details-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[SchedulePolicyUpdateResponse](#schemaschedulepolicyupdateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Enumerate returns a list of schedule policy

<a id="opIdSchedulePolicy_Enumerate"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/schedulepolicy/{org_id} \
  -H 'Accept: application/json'

```

`GET /v1/schedulepolicy/{org_id}`

<h4 id="enumerate-returns-a-list-of-schedule-policy-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "schedule_policies": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "schedule_policy_info": {
        "interval": {
          "minutes": "string",
          "retain": "string"
        },
        "daily": {
          "time": "string",
          "retain": "string"
        },
        "weekly": {
          "day": "string",
          "time": "string",
          "retain": "string"
        },
        "monthly": {
          "date": "string",
          "time": "string",
          "retain": "string"
        },
        "backup_schedule": [
          "string"
        ]
      }
    }
  ]
}
```

<h4 id="enumerate-returns-a-list-of-schedule-policy-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[SchedulePolicyEnumerateResponse](#schemaschedulepolicyenumerateresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Inspect returns detail information about a specified schedule policy

<a id="opIdSchedulePolicy_Inspect"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/schedulepolicy/{org_id}/{name} \
  -H 'Accept: application/json'

```

`GET /v1/schedulepolicy/{org_id}/{name}`

<h4 id="inspect-returns-detail-information-about-a-specified-schedule-policy-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{
  "schedule_policy": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "schedule_policy_info": {
      "interval": {
        "minutes": "string",
        "retain": "string"
      },
      "daily": {
        "time": "string",
        "retain": "string"
      },
      "weekly": {
        "day": "string",
        "time": "string",
        "retain": "string"
      },
      "monthly": {
        "date": "string",
        "time": "string",
        "retain": "string"
      },
      "backup_schedule": [
        "string"
      ]
    }
  }
}
```

<h4 id="inspect-returns-detail-information-about-a-specified-schedule-policy-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[SchedulePolicyInspectResponse](#schemaschedulepolicyinspectresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

## Delete removes a schedule policy

<a id="opIdSchedulePolicy_Delete"></a>

#### Code sample

```shell
# You can also use wget
curl -X DELETE /v1/schedulepolicy/{org_id}/{name} \
  -H 'Accept: application/json'

```

`DELETE /v1/schedulepolicy/{org_id}/{name}`

<h4 id="delete-removes-a-schedule-policy-parameters">Parameters</h4>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|org_id|path|string|true|none|
|name|path|string|true|none|

#### Example response

_200 Response_

```json
{}
```

<h4 id="delete-removes-a-schedule-policy-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[SchedulePolicyDeleteResponse](#schemaschedulepolicydeleteresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="pkg-apis-v1-api-proto-version">Version</h1>

## Get gets the version of the server

<a id="opIdVersion_Get"></a>

#### Code sample

```shell
# You can also use wget
curl -X GET /v1/version \
  -H 'Accept: application/json'

```

`GET /v1/version`

#### Example response

_200 Response_

```json
{
  "version": {
    "major": "string",
    "minor": "string",
    "patch": "string",
    "git_commit": "string",
    "build_date": "string"
  }
}
```

<h4 id="get-gets-the-version-of-the-server-responses">Responses</h4>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A successful response.|[VersionGetResponse](#schemaversiongetresponse)|
|default|Default|An unexpected error response|[runtimeError](#schemaruntimeerror)|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_AWSConfig">AWSConfig</h2>
<!-- backwards compatibility -->
<a id="schemaawsconfig"></a>
<a id="schema_AWSConfig"></a>
<a id="tocSawsconfig"></a>
<a id="tocsawsconfig"></a>

```json
{
  "access_key": "string",
  "secret_key": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|access_key|string|false|none|none|
|secret_key|string|false|none|none|

<h2 id="tocS_AzureConfig">AzureConfig</h2>
<!-- backwards compatibility -->
<a id="schemaazureconfig"></a>
<a id="schema_AzureConfig"></a>
<a id="tocSazureconfig"></a>
<a id="tocsazureconfig"></a>

```json
{
  "account_name": "string",
  "account_key": "string",
  "client_secret": "string",
  "client_id": "string",
  "tenant_id": "string",
  "subscription_id": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|account_name|string|false|none|none|
|account_key|string|false|none|none|
|client_secret|string|false|none|none|
|client_id|string|false|none|none|
|tenant_id|string|false|none|none|
|subscription_id|string|false|none|TODO: Need to see if this has to be here or in the backup object.|

<h2 id="tocS_BackupCreateRequest">BackupCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemabackupcreaterequest"></a>
<a id="schema_BackupCreateRequest"></a>
<a id="tocSbackupcreaterequest"></a>
<a id="tocsbackupcreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "pre_exec_rule": "string",
  "post_exec_rule": "string"
}

```

Request message structure for backup create

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|backup_location|string|false|none|none|
|cluster|string|false|none|none|
|namespaces|[string]|false|none|none|
|label_selectors|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|pre_exec_rule|string|false|none|none|
|post_exec_rule|string|false|none|none|

<h2 id="tocS_BackupCreateResponse">BackupCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupcreateresponse"></a>
<a id="schema_BackupCreateResponse"></a>
<a id="tocSbackupcreateresponse"></a>
<a id="tocsbackupcreateresponse"></a>

```json
{}

```

Response message structure for backup create

### Properties

*None*

<h2 id="tocS_BackupDeleteResponse">BackupDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupdeleteresponse"></a>
<a id="schema_BackupDeleteResponse"></a>
<a id="tocSbackupdeleteresponse"></a>
<a id="tocsbackupdeleteresponse"></a>

```json
{}

```

Response message strcuture for object delete

### Properties

*None*

<h2 id="tocS_BackupEnumerateResponse">BackupEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupenumerateresponse"></a>
<a id="schema_BackupEnumerateResponse"></a>
<a id="tocSbackupenumerateresponse"></a>
<a id="tocsbackupenumerateresponse"></a>

```json
{
  "backups": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "backup_info": {
        "backup_location": "string",
        "cluster": "string",
        "namespaces": [
          "string"
        ],
        "label_selectors": {
          "property1": "string",
          "property2": "string"
        },
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "resources": [
          {
            "name": "string",
            "namespace": "string",
            "group": "string",
            "kind": "string",
            "version": "string"
          }
        ],
        "volumes": [
          {
            "name": "string",
            "namespace": "string",
            "pvc": "string",
            "backup_id": "string",
            "status": {
              "status": "Invalid",
              "reason": "string"
            },
            "driver_name": "string",
            "zones": [
              "string"
            ],
            "options": {
              "property1": "string",
              "property2": "string"
            }
          }
        ],
        "backup_path": "string",
        "stage": "Invalid",
        "pre_exec_rule": "string",
        "post_exec_rule": "string",
        "backup_schedule": {
          "uid": "string",
          "name": "string"
        },
        "cr_name": "string"
      }
    }
  ],
  "continuation_token": "string"
}

```

Response message structure for enumerate create

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backups|[[BackupObject](#schemabackupobject)]|false|none|[Message for Backup object which will be stored in Datastore.]|
|continuation_token|string|false|none|none|

<h2 id="tocS_BackupInfo">BackupInfo</h2>
<!-- backwards compatibility -->
<a id="schemabackupinfo"></a>
<a id="schema_BackupInfo"></a>
<a id="tocSbackupinfo"></a>
<a id="tocsbackupinfo"></a>

```json
{
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "status": {
    "status": "Invalid",
    "reason": "string"
  },
  "resources": [
    {
      "name": "string",
      "namespace": "string",
      "group": "string",
      "kind": "string",
      "version": "string"
    }
  ],
  "volumes": [
    {
      "name": "string",
      "namespace": "string",
      "pvc": "string",
      "backup_id": "string",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "driver_name": "string",
      "zones": [
        "string"
      ],
      "options": {
        "property1": "string",
        "property2": "string"
      }
    }
  ],
  "backup_path": "string",
  "stage": "Invalid",
  "pre_exec_rule": "string",
  "post_exec_rule": "string",
  "backup_schedule": {
    "uid": "string",
    "name": "string"
  },
  "cr_name": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup_location|string|false|none|none|
|cluster|string|false|none|none|
|namespaces|[string]|false|none|none|
|label_selectors|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|status|[BackupInfoStatusInfo](#schemabackupinfostatusinfo)|false|none|Message for maintaing status of the object.|
|resources|[[BackupInfoResource](#schemabackupinforesource)]|false|none|none|
|volumes|[[BackupInfoVolume](#schemabackupinfovolume)]|false|none|none|
|backup_path|string|false|none|none|
|stage|[BackupInfoStage](#schemabackupinfostage)|false|none|none|
|pre_exec_rule|string|false|none|none|
|post_exec_rule|string|false|none|none|
|backup_schedule|[BackupInfoBackupSchedule](#schemabackupinfobackupschedule)|false|none|none|
|cr_name|string|false|none|none|

<h2 id="tocS_BackupInfoBackupSchedule">BackupInfoBackupSchedule</h2>
<!-- backwards compatibility -->
<a id="schemabackupinfobackupschedule"></a>
<a id="schema_BackupInfoBackupSchedule"></a>
<a id="tocSbackupinfobackupschedule"></a>
<a id="tocsbackupinfobackupschedule"></a>

```json
{
  "uid": "string",
  "name": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|uid|string|false|none|none|
|name|string|false|none|none|

<h2 id="tocS_BackupInfoResource">BackupInfoResource</h2>
<!-- backwards compatibility -->
<a id="schemabackupinforesource"></a>
<a id="schema_BackupInfoResource"></a>
<a id="tocSbackupinforesource"></a>
<a id="tocsbackupinforesource"></a>

```json
{
  "name": "string",
  "namespace": "string",
  "group": "string",
  "kind": "string",
  "version": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|namespace|string|false|none|none|
|group|string|false|none|none|
|kind|string|false|none|none|
|version|string|false|none|none|

<h2 id="tocS_BackupInfoStage">BackupInfoStage</h2>
<!-- backwards compatibility -->
<a id="schemabackupinfostage"></a>
<a id="schema_BackupInfoStage"></a>
<a id="tocSbackupinfostage"></a>
<a id="tocsbackupinfostage"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Initial|
|*anonymous*|PreExecRule|
|*anonymous*|PostExecRule|
|*anonymous*|Volumes|
|*anonymous*|Applications|
|*anonymous*|Final|

<h2 id="tocS_BackupInfoStatusInfo">BackupInfoStatusInfo</h2>
<!-- backwards compatibility -->
<a id="schemabackupinfostatusinfo"></a>
<a id="schema_BackupInfoStatusInfo"></a>
<a id="tocSbackupinfostatusinfo"></a>
<a id="tocsbackupinfostatusinfo"></a>

```json
{
  "status": "Invalid",
  "reason": "string"
}

```

Message for maintaing status of the object.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|[BackupInfoStatusInfoStatus](#schemabackupinfostatusinfostatus)|false|none|none|
|reason|string|false|none|none|

<h2 id="tocS_BackupInfoStatusInfoStatus">BackupInfoStatusInfoStatus</h2>
<!-- backwards compatibility -->
<a id="schemabackupinfostatusinfostatus"></a>
<a id="schema_BackupInfoStatusInfoStatus"></a>
<a id="tocSbackupinfostatusinfostatus"></a>
<a id="tocsbackupinfostatusinfostatus"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Pending|
|*anonymous*|InProgress|
|*anonymous*|Aborted|
|*anonymous*|Failed|
|*anonymous*|Deleting|
|*anonymous*|Success|
|*anonymous*|Captured|
|*anonymous*|PartialSuccess|
|*anonymous*|DeletePending|

<h2 id="tocS_BackupInfoVolume">BackupInfoVolume</h2>
<!-- backwards compatibility -->
<a id="schemabackupinfovolume"></a>
<a id="schema_BackupInfoVolume"></a>
<a id="tocSbackupinfovolume"></a>
<a id="tocsbackupinfovolume"></a>

```json
{
  "name": "string",
  "namespace": "string",
  "pvc": "string",
  "backup_id": "string",
  "status": {
    "status": "Invalid",
    "reason": "string"
  },
  "driver_name": "string",
  "zones": [
    "string"
  ],
  "options": {
    "property1": "string",
    "property2": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|namespace|string|false|none|none|
|pvc|string|false|none|none|
|backup_id|string|false|none|none|
|status|[BackupInfoStatusInfo](#schemabackupinfostatusinfo)|false|none|Message for maintaing status of the object.|
|driver_name|string|false|none|none|
|zones|[string]|false|none|none|
|options|object|false|none|none|
|» **additionalProperties**|string|false|none|none|

<h2 id="tocS_BackupInspectResponse">BackupInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupinspectresponse"></a>
<a id="schema_BackupInspectResponse"></a>
<a id="tocSbackupinspectresponse"></a>
<a id="tocsbackupinspectresponse"></a>

```json
{
  "backup": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "backup_info": {
      "backup_location": "string",
      "cluster": "string",
      "namespaces": [
        "string"
      ],
      "label_selectors": {
        "property1": "string",
        "property2": "string"
      },
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "resources": [
        {
          "name": "string",
          "namespace": "string",
          "group": "string",
          "kind": "string",
          "version": "string"
        }
      ],
      "volumes": [
        {
          "name": "string",
          "namespace": "string",
          "pvc": "string",
          "backup_id": "string",
          "status": {
            "status": "Invalid",
            "reason": "string"
          },
          "driver_name": "string",
          "zones": [
            "string"
          ],
          "options": {
            "property1": "string",
            "property2": "string"
          }
        }
      ],
      "backup_path": "string",
      "stage": "Invalid",
      "pre_exec_rule": "string",
      "post_exec_rule": "string",
      "backup_schedule": {
        "uid": "string",
        "name": "string"
      },
      "cr_name": "string"
    }
  }
}

```

Response message strcuture for object inspect

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup|[BackupObject](#schemabackupobject)|false|none|Message for Backup object which will be stored in Datastore.|

<h2 id="tocS_BackupLocationCreateRequest">BackupLocationCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationcreaterequest"></a>
<a id="schema_BackupLocationCreateRequest"></a>
<a id="tocSbackuplocationcreaterequest"></a>
<a id="tocsbackuplocationcreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_location": {
    "type": "Invalid",
    "path": "string",
    "encryption_key": "string",
    "cloud_credential": "string",
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "delete_backups": true,
    "s3_config": {
      "endpoint": "string",
      "region": "string",
      "disable_ssl": true,
      "disable_path_style": true
    }
  }
}

```

Define BackupLocationCreateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|backup_location|[BackupLocationInfo](#schemabackuplocationinfo)|false|none|none|

<h2 id="tocS_BackupLocationCreateResponse">BackupLocationCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationcreateresponse"></a>
<a id="schema_BackupLocationCreateResponse"></a>
<a id="tocSbackuplocationcreateresponse"></a>
<a id="tocsbackuplocationcreateresponse"></a>

```json
{}

```

Define BackupLocationCreateResponse struct

### Properties

*None*

<h2 id="tocS_BackupLocationDeleteResponse">BackupLocationDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationdeleteresponse"></a>
<a id="schema_BackupLocationDeleteResponse"></a>
<a id="tocSbackuplocationdeleteresponse"></a>
<a id="tocsbackuplocationdeleteresponse"></a>

```json
{}

```

Define BackupLocationInspectResponse struct

### Properties

*None*

<h2 id="tocS_BackupLocationEnumerateResponse">BackupLocationEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationenumerateresponse"></a>
<a id="schema_BackupLocationEnumerateResponse"></a>
<a id="tocSbackuplocationenumerateresponse"></a>
<a id="tocsbackuplocationenumerateresponse"></a>

```json
{
  "backup_locations": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "backup_location_info": {
        "type": "Invalid",
        "path": "string",
        "encryption_key": "string",
        "cloud_credential": "string",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "delete_backups": true,
        "s3_config": {
          "endpoint": "string",
          "region": "string",
          "disable_ssl": true,
          "disable_path_style": true
        }
      }
    }
  ]
}

```

Define BackupLocationEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup_locations|[[BackupLocationObject](#schemabackuplocationobject)]|false|none|none|

<h2 id="tocS_BackupLocationInfo">BackupLocationInfo</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationinfo"></a>
<a id="schema_BackupLocationInfo"></a>
<a id="tocSbackuplocationinfo"></a>
<a id="tocsbackuplocationinfo"></a>

```json
{
  "type": "Invalid",
  "path": "string",
  "encryption_key": "string",
  "cloud_credential": "string",
  "status": {
    "status": "Invalid",
    "reason": "string"
  },
  "delete_backups": true,
  "s3_config": {
    "endpoint": "string",
    "region": "string",
    "disable_ssl": true,
    "disable_path_style": true
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|[BackupLocationInfoType](#schemabackuplocationinfotype)|false|none|none|
|path|string|false|none|none|
|encryption_key|string|false|none|none|
|cloud_credential|string|false|none|none|
|status|[BackupLocationInfoStatusInfo](#schemabackuplocationinfostatusinfo)|false|none|Message for maintaing status of the object.|
|delete_backups|boolean(boolean)|false|none|none|
|s3_config|[S3Config](#schemas3config)|false|none|none|

<h2 id="tocS_BackupLocationInfoStatusInfo">BackupLocationInfoStatusInfo</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationinfostatusinfo"></a>
<a id="schema_BackupLocationInfoStatusInfo"></a>
<a id="tocSbackuplocationinfostatusinfo"></a>
<a id="tocsbackuplocationinfostatusinfo"></a>

```json
{
  "status": "Invalid",
  "reason": "string"
}

```

Message for maintaing status of the object.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|[BackupLocationInfoStatusInfoStatus](#schemabackuplocationinfostatusinfostatus)|false|none|none|
|reason|string|false|none|none|

<h2 id="tocS_BackupLocationInfoStatusInfoStatus">BackupLocationInfoStatusInfoStatus</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationinfostatusinfostatus"></a>
<a id="schema_BackupLocationInfoStatusInfoStatus"></a>
<a id="tocSbackuplocationinfostatusinfostatus"></a>
<a id="tocsbackuplocationinfostatusinfostatus"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Valid|
|*anonymous*|DeletePending|

<h2 id="tocS_BackupLocationInfoType">BackupLocationInfoType</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationinfotype"></a>
<a id="schema_BackupLocationInfoType"></a>
<a id="tocSbackuplocationinfotype"></a>
<a id="tocsbackuplocationinfotype"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|S3|
|*anonymous*|Azure|
|*anonymous*|Google|

<h2 id="tocS_BackupLocationInspectResponse">BackupLocationInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationinspectresponse"></a>
<a id="schema_BackupLocationInspectResponse"></a>
<a id="tocSbackuplocationinspectresponse"></a>
<a id="tocsbackuplocationinspectresponse"></a>

```json
{
  "backup_location": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "backup_location_info": {
      "type": "Invalid",
      "path": "string",
      "encryption_key": "string",
      "cloud_credential": "string",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "delete_backups": true,
      "s3_config": {
        "endpoint": "string",
        "region": "string",
        "disable_ssl": true,
        "disable_path_style": true
      }
    }
  }
}

```

Define BackupLocationInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup_location|[BackupLocationObject](#schemabackuplocationobject)|false|none|none|

<h2 id="tocS_BackupLocationObject">BackupLocationObject</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationobject"></a>
<a id="schema_BackupLocationObject"></a>
<a id="tocSbackuplocationobject"></a>
<a id="tocsbackuplocationobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_location_info": {
    "type": "Invalid",
    "path": "string",
    "encryption_key": "string",
    "cloud_credential": "string",
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "delete_backups": true,
    "s3_config": {
      "endpoint": "string",
      "region": "string",
      "disable_ssl": true,
      "disable_path_style": true
    }
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|backup_location_info|[BackupLocationInfo](#schemabackuplocationinfo)|false|none|none|

<h2 id="tocS_BackupLocationUpdateRequest">BackupLocationUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationupdaterequest"></a>
<a id="schema_BackupLocationUpdateRequest"></a>
<a id="tocSbackuplocationupdaterequest"></a>
<a id="tocsbackuplocationupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_location": {
    "type": "Invalid",
    "path": "string",
    "encryption_key": "string",
    "cloud_credential": "string",
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "delete_backups": true,
    "s3_config": {
      "endpoint": "string",
      "region": "string",
      "disable_ssl": true,
      "disable_path_style": true
    }
  }
}

```

Define BackupLocationUpdateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|backup_location|[BackupLocationInfo](#schemabackuplocationinfo)|false|none|none|

<h2 id="tocS_BackupLocationUpdateResponse">BackupLocationUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackuplocationupdateresponse"></a>
<a id="schema_BackupLocationUpdateResponse"></a>
<a id="tocSbackuplocationupdateresponse"></a>
<a id="tocsbackuplocationupdateresponse"></a>

```json
{}

```

Define BackupLocationUpdateResponse struct

### Properties

*None*

<h2 id="tocS_BackupObject">BackupObject</h2>
<!-- backwards compatibility -->
<a id="schemabackupobject"></a>
<a id="schema_BackupObject"></a>
<a id="tocSbackupobject"></a>
<a id="tocsbackupobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_info": {
    "backup_location": "string",
    "cluster": "string",
    "namespaces": [
      "string"
    ],
    "label_selectors": {
      "property1": "string",
      "property2": "string"
    },
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "resources": [
      {
        "name": "string",
        "namespace": "string",
        "group": "string",
        "kind": "string",
        "version": "string"
      }
    ],
    "volumes": [
      {
        "name": "string",
        "namespace": "string",
        "pvc": "string",
        "backup_id": "string",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "driver_name": "string",
        "zones": [
          "string"
        ],
        "options": {
          "property1": "string",
          "property2": "string"
        }
      }
    ],
    "backup_path": "string",
    "stage": "Invalid",
    "pre_exec_rule": "string",
    "post_exec_rule": "string",
    "backup_schedule": {
      "uid": "string",
      "name": "string"
    },
    "cr_name": "string"
  }
}

```

Message for Backup object which will be stored in Datastore.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|backup_info|[BackupInfo](#schemabackupinfo)|false|none|none|

<h2 id="tocS_BackupScheduleCreateRequest">BackupScheduleCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemabackupschedulecreaterequest"></a>
<a id="schema_BackupScheduleCreateRequest"></a>
<a id="tocSbackupschedulecreaterequest"></a>
<a id="tocsbackupschedulecreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": "string",
  "reclaim_policy": "Invalid",
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "pre_exec_rule": "string",
  "post_exec_rule": "string"
}

```

Define BackupScheduleCreateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|schedule_policy|string|false|none|none|
|reclaim_policy|[BackupScheduleInfoReclaimPolicyType](#schemabackupscheduleinforeclaimpolicytype)|false|none|none|
|backup_location|string|false|none|none|
|cluster|string|false|none|none|
|namespaces|[string]|false|none|none|
|label_selectors|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|pre_exec_rule|string|false|none|none|
|post_exec_rule|string|false|none|none|

<h2 id="tocS_BackupScheduleCreateResponse">BackupScheduleCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupschedulecreateresponse"></a>
<a id="schema_BackupScheduleCreateResponse"></a>
<a id="tocSbackupschedulecreateresponse"></a>
<a id="tocsbackupschedulecreateresponse"></a>

```json
{}

```

Define BackupScheduleCreateResponse struct

### Properties

*None*

<h2 id="tocS_BackupScheduleDeleteResponse">BackupScheduleDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduledeleteresponse"></a>
<a id="schema_BackupScheduleDeleteResponse"></a>
<a id="tocSbackupscheduledeleteresponse"></a>
<a id="tocsbackupscheduledeleteresponse"></a>

```json
{}

```

Define BackupScheduleDeleteResponse struct

### Properties

*None*

<h2 id="tocS_BackupScheduleEnumerateResponse">BackupScheduleEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleenumerateresponse"></a>
<a id="schema_BackupScheduleEnumerateResponse"></a>
<a id="tocSbackupscheduleenumerateresponse"></a>
<a id="tocsbackupscheduleenumerateresponse"></a>

```json
{
  "backup_schedules": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "backup_schedule_info": {
        "schedule_policy": "string",
        "suspend": true,
        "reclaim_policy": "Invalid",
        "backup_status": {
          "property1": {
            "status": [
              {
                "backup_name": "string",
                "create_time": "2020-04-29T05:40:19Z",
                "finish_time": "2020-04-29T05:40:19Z",
                "status": "Invalid"
              }
            ]
          },
          "property2": {
            "status": [
              {
                "backup_name": "string",
                "create_time": "2020-04-29T05:40:19Z",
                "finish_time": "2020-04-29T05:40:19Z",
                "status": "Invalid"
              }
            ]
          }
        },
        "backup_location": "string",
        "cluster": "string",
        "namespaces": [
          "string"
        ],
        "label_selectors": {
          "property1": "string",
          "property2": "string"
        },
        "pre_exec_rule": "string",
        "post_exec_rule": "string",
        "delete_backups": true,
        "status": {
          "backup_name": "string",
          "create_time": "2020-04-29T05:40:19Z",
          "finish_time": "2020-04-29T05:40:19Z",
          "status": "Invalid"
        },
        "suspended_by": {
          "source": "Invalid"
        }
      }
    }
  ]
}

```

Define BackupScheduleEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup_schedules|[[BackupScheduleObject](#schemabackupscheduleobject)]|false|none|none|

<h2 id="tocS_BackupScheduleInfo">BackupScheduleInfo</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleinfo"></a>
<a id="schema_BackupScheduleInfo"></a>
<a id="tocSbackupscheduleinfo"></a>
<a id="tocsbackupscheduleinfo"></a>

```json
{
  "schedule_policy": "string",
  "suspend": true,
  "reclaim_policy": "Invalid",
  "backup_status": {
    "property1": {
      "status": [
        {
          "backup_name": "string",
          "create_time": "2020-04-29T05:40:19Z",
          "finish_time": "2020-04-29T05:40:19Z",
          "status": "Invalid"
        }
      ]
    },
    "property2": {
      "status": [
        {
          "backup_name": "string",
          "create_time": "2020-04-29T05:40:19Z",
          "finish_time": "2020-04-29T05:40:19Z",
          "status": "Invalid"
        }
      ]
    }
  },
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "pre_exec_rule": "string",
  "post_exec_rule": "string",
  "delete_backups": true,
  "status": {
    "backup_name": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "finish_time": "2020-04-29T05:40:19Z",
    "status": "Invalid"
  },
  "suspended_by": {
    "source": "Invalid"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|schedule_policy|string|false|none|none|
|suspend|boolean(boolean)|false|none|none|
|reclaim_policy|[BackupScheduleInfoReclaimPolicyType](#schemabackupscheduleinforeclaimpolicytype)|false|none|none|
|backup_status|object|false|none|none|
|» **additionalProperties**|[BackupScheduleInfoStatusInfoList](#schemabackupscheduleinfostatusinfolist)|false|none|none|
|backup_location|string|false|none|none|
|cluster|string|false|none|none|
|namespaces|[string]|false|none|none|
|label_selectors|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|pre_exec_rule|string|false|none|none|
|post_exec_rule|string|false|none|none|
|delete_backups|boolean(boolean)|false|none|none|
|status|[BackupScheduleInfoStatusInfo](#schemabackupscheduleinfostatusinfo)|false|none|none|
|suspended_by|[BackupScheduleInfoSuspendedBy](#schemabackupscheduleinfosuspendedby)|false|none|none|

<h2 id="tocS_BackupScheduleInfoReclaimPolicyType">BackupScheduleInfoReclaimPolicyType</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleinforeclaimpolicytype"></a>
<a id="schema_BackupScheduleInfoReclaimPolicyType"></a>
<a id="tocSbackupscheduleinforeclaimpolicytype"></a>
<a id="tocsbackupscheduleinforeclaimpolicytype"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Delete|
|*anonymous*|Retain|

<h2 id="tocS_BackupScheduleInfoStatusInfo">BackupScheduleInfoStatusInfo</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleinfostatusinfo"></a>
<a id="schema_BackupScheduleInfoStatusInfo"></a>
<a id="tocSbackupscheduleinfostatusinfo"></a>
<a id="tocsbackupscheduleinfostatusinfo"></a>

```json
{
  "backup_name": "string",
  "create_time": "2020-04-29T05:40:19Z",
  "finish_time": "2020-04-29T05:40:19Z",
  "status": "Invalid"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup_name|string|false|none|none|
|create_time|string(date-time)|false|none|none|
|finish_time|string(date-time)|false|none|none|
|status|[BackupScheduleInfoStatusInfoStatus](#schemabackupscheduleinfostatusinfostatus)|false|none|none|

<h2 id="tocS_BackupScheduleInfoStatusInfoList">BackupScheduleInfoStatusInfoList</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleinfostatusinfolist"></a>
<a id="schema_BackupScheduleInfoStatusInfoList"></a>
<a id="tocSbackupscheduleinfostatusinfolist"></a>
<a id="tocsbackupscheduleinfostatusinfolist"></a>

```json
{
  "status": [
    {
      "backup_name": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "finish_time": "2020-04-29T05:40:19Z",
      "status": "Invalid"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|[[BackupScheduleInfoStatusInfo](#schemabackupscheduleinfostatusinfo)]|false|none|none|

<h2 id="tocS_BackupScheduleInfoStatusInfoStatus">BackupScheduleInfoStatusInfoStatus</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleinfostatusinfostatus"></a>
<a id="schema_BackupScheduleInfoStatusInfoStatus"></a>
<a id="tocSbackupscheduleinfostatusinfostatus"></a>
<a id="tocsbackupscheduleinfostatusinfostatus"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Pending|
|*anonymous*|InProgress|
|*anonymous*|Aborted|
|*anonymous*|Failed|
|*anonymous*|Deleting|
|*anonymous*|Success|
|*anonymous*|Captured|
|*anonymous*|PartialSuccess|
|*anonymous*|DeletePending|

<h2 id="tocS_BackupScheduleInfoSuspendedBy">BackupScheduleInfoSuspendedBy</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleinfosuspendedby"></a>
<a id="schema_BackupScheduleInfoSuspendedBy"></a>
<a id="tocSbackupscheduleinfosuspendedby"></a>
<a id="tocsbackupscheduleinfosuspendedby"></a>

```json
{
  "source": "Invalid"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|source|[SuspendedBySource](#schemasuspendedbysource)|false|none|none|

<h2 id="tocS_BackupScheduleInspectResponse">BackupScheduleInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleinspectresponse"></a>
<a id="schema_BackupScheduleInspectResponse"></a>
<a id="tocSbackupscheduleinspectresponse"></a>
<a id="tocsbackupscheduleinspectresponse"></a>

```json
{
  "backup_schedule": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "backup_schedule_info": {
      "schedule_policy": "string",
      "suspend": true,
      "reclaim_policy": "Invalid",
      "backup_status": {
        "property1": {
          "status": [
            {
              "backup_name": "string",
              "create_time": "2020-04-29T05:40:19Z",
              "finish_time": "2020-04-29T05:40:19Z",
              "status": "Invalid"
            }
          ]
        },
        "property2": {
          "status": [
            {
              "backup_name": "string",
              "create_time": "2020-04-29T05:40:19Z",
              "finish_time": "2020-04-29T05:40:19Z",
              "status": "Invalid"
            }
          ]
        }
      },
      "backup_location": "string",
      "cluster": "string",
      "namespaces": [
        "string"
      ],
      "label_selectors": {
        "property1": "string",
        "property2": "string"
      },
      "pre_exec_rule": "string",
      "post_exec_rule": "string",
      "delete_backups": true,
      "status": {
        "backup_name": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "finish_time": "2020-04-29T05:40:19Z",
        "status": "Invalid"
      },
      "suspended_by": {
        "source": "Invalid"
      }
    }
  }
}

```

Define BackupScheduleInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup_schedule|[BackupScheduleObject](#schemabackupscheduleobject)|false|none|none|

<h2 id="tocS_BackupScheduleObject">BackupScheduleObject</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleobject"></a>
<a id="schema_BackupScheduleObject"></a>
<a id="tocSbackupscheduleobject"></a>
<a id="tocsbackupscheduleobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup_schedule_info": {
    "schedule_policy": "string",
    "suspend": true,
    "reclaim_policy": "Invalid",
    "backup_status": {
      "property1": {
        "status": [
          {
            "backup_name": "string",
            "create_time": "2020-04-29T05:40:19Z",
            "finish_time": "2020-04-29T05:40:19Z",
            "status": "Invalid"
          }
        ]
      },
      "property2": {
        "status": [
          {
            "backup_name": "string",
            "create_time": "2020-04-29T05:40:19Z",
            "finish_time": "2020-04-29T05:40:19Z",
            "status": "Invalid"
          }
        ]
      }
    },
    "backup_location": "string",
    "cluster": "string",
    "namespaces": [
      "string"
    ],
    "label_selectors": {
      "property1": "string",
      "property2": "string"
    },
    "pre_exec_rule": "string",
    "post_exec_rule": "string",
    "delete_backups": true,
    "status": {
      "backup_name": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "finish_time": "2020-04-29T05:40:19Z",
      "status": "Invalid"
    },
    "suspended_by": {
      "source": "Invalid"
    }
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|backup_schedule_info|[BackupScheduleInfo](#schemabackupscheduleinfo)|false|none|none|

<h2 id="tocS_BackupScheduleUpdateRequest">BackupScheduleUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleupdaterequest"></a>
<a id="schema_BackupScheduleUpdateRequest"></a>
<a id="tocSbackupscheduleupdaterequest"></a>
<a id="tocsbackupscheduleupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": "string",
  "reclaim_policy": "Invalid",
  "backup_location": "string",
  "cluster": "string",
  "namespaces": [
    "string"
  ],
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "pre_exec_rule": "string",
  "post_exec_rule": "string",
  "suspend": true
}

```

Define BackupScheduleUpdateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|schedule_policy|string|false|none|none|
|reclaim_policy|[BackupScheduleInfoReclaimPolicyType](#schemabackupscheduleinforeclaimpolicytype)|false|none|none|
|backup_location|string|false|none|none|
|cluster|string|false|none|none|
|namespaces|[string]|false|none|none|
|label_selectors|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|pre_exec_rule|string|false|none|none|
|post_exec_rule|string|false|none|none|
|suspend|boolean(boolean)|false|none|none|

<h2 id="tocS_BackupScheduleUpdateResponse">BackupScheduleUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupscheduleupdateresponse"></a>
<a id="schema_BackupScheduleUpdateResponse"></a>
<a id="tocSbackupscheduleupdateresponse"></a>
<a id="tocsbackupscheduleupdateresponse"></a>

```json
{}

```

Define BackupScheduleUpdateResponse struct

### Properties

*None*

<h2 id="tocS_BackupUpdateRequest">BackupUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemabackupupdaterequest"></a>
<a id="schema_BackupUpdateRequest"></a>
<a id="tocSbackupupdaterequest"></a>
<a id="tocsbackupupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  }
}

```

Define BackupUpdateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|

<h2 id="tocS_BackupUpdateResponse">BackupUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemabackupupdateresponse"></a>
<a id="schema_BackupUpdateResponse"></a>
<a id="tocSbackupupdateresponse"></a>
<a id="tocsbackupupdateresponse"></a>

```json
{}

```

Define BackupUpdateResponse struct

### Properties

*None*

<h2 id="tocS_CloudCredentialCreateRequest">CloudCredentialCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialcreaterequest"></a>
<a id="schema_CloudCredentialCreateRequest"></a>
<a id="tocScloudcredentialcreaterequest"></a>
<a id="tocscloudcredentialcreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "cloud_credential": {
    "type": "Invalid",
    "aws_config": {
      "access_key": "string",
      "secret_key": "string"
    },
    "azure_config": {
      "account_name": "string",
      "account_key": "string",
      "client_secret": "string",
      "client_id": "string",
      "tenant_id": "string",
      "subscription_id": "string"
    },
    "google_config": {
      "project_id": "string",
      "json_key": "string"
    }
  }
}

```

Define CloudCredentialCreateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|cloud_credential|[CloudCredentialInfo](#schemacloudcredentialinfo)|false|none|none|

<h2 id="tocS_CloudCredentialCreateResponse">CloudCredentialCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialcreateresponse"></a>
<a id="schema_CloudCredentialCreateResponse"></a>
<a id="tocScloudcredentialcreateresponse"></a>
<a id="tocscloudcredentialcreateresponse"></a>

```json
{}

```

Define CloudCredentialCreateResponse struct

### Properties

*None*

<h2 id="tocS_CloudCredentialDeleteResponse">CloudCredentialDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialdeleteresponse"></a>
<a id="schema_CloudCredentialDeleteResponse"></a>
<a id="tocScloudcredentialdeleteresponse"></a>
<a id="tocscloudcredentialdeleteresponse"></a>

```json
{}

```

Define CloudCredentialInspectResponse struct

### Properties

*None*

<h2 id="tocS_CloudCredentialEnumerateResponse">CloudCredentialEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialenumerateresponse"></a>
<a id="schema_CloudCredentialEnumerateResponse"></a>
<a id="tocScloudcredentialenumerateresponse"></a>
<a id="tocscloudcredentialenumerateresponse"></a>

```json
{
  "cloud_credentials": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "cloud_credential_info": {
        "type": "Invalid",
        "aws_config": {
          "access_key": "string",
          "secret_key": "string"
        },
        "azure_config": {
          "account_name": "string",
          "account_key": "string",
          "client_secret": "string",
          "client_id": "string",
          "tenant_id": "string",
          "subscription_id": "string"
        },
        "google_config": {
          "project_id": "string",
          "json_key": "string"
        }
      }
    }
  ]
}

```

Define CloudCredentialEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|cloud_credentials|[[CloudCredentialObject](#schemacloudcredentialobject)]|false|none|none|

<h2 id="tocS_CloudCredentialInfo">CloudCredentialInfo</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialinfo"></a>
<a id="schema_CloudCredentialInfo"></a>
<a id="tocScloudcredentialinfo"></a>
<a id="tocscloudcredentialinfo"></a>

```json
{
  "type": "Invalid",
  "aws_config": {
    "access_key": "string",
    "secret_key": "string"
  },
  "azure_config": {
    "account_name": "string",
    "account_key": "string",
    "client_secret": "string",
    "client_id": "string",
    "tenant_id": "string",
    "subscription_id": "string"
  },
  "google_config": {
    "project_id": "string",
    "json_key": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|[CloudCredentialInfoType](#schemacloudcredentialinfotype)|false|none|none|
|aws_config|[AWSConfig](#schemaawsconfig)|false|none|none|
|azure_config|[AzureConfig](#schemaazureconfig)|false|none|none|
|google_config|[GoogleConfig](#schemagoogleconfig)|false|none|none|

<h2 id="tocS_CloudCredentialInfoType">CloudCredentialInfoType</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialinfotype"></a>
<a id="schema_CloudCredentialInfoType"></a>
<a id="tocScloudcredentialinfotype"></a>
<a id="tocscloudcredentialinfotype"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|AWS|
|*anonymous*|Azure|
|*anonymous*|Google|

<h2 id="tocS_CloudCredentialInspectResponse">CloudCredentialInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialinspectresponse"></a>
<a id="schema_CloudCredentialInspectResponse"></a>
<a id="tocScloudcredentialinspectresponse"></a>
<a id="tocscloudcredentialinspectresponse"></a>

```json
{
  "cloud_credential": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "cloud_credential_info": {
      "type": "Invalid",
      "aws_config": {
        "access_key": "string",
        "secret_key": "string"
      },
      "azure_config": {
        "account_name": "string",
        "account_key": "string",
        "client_secret": "string",
        "client_id": "string",
        "tenant_id": "string",
        "subscription_id": "string"
      },
      "google_config": {
        "project_id": "string",
        "json_key": "string"
      }
    }
  }
}

```

Define CloudCredentialInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|cloud_credential|[CloudCredentialObject](#schemacloudcredentialobject)|false|none|none|

<h2 id="tocS_CloudCredentialObject">CloudCredentialObject</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialobject"></a>
<a id="schema_CloudCredentialObject"></a>
<a id="tocScloudcredentialobject"></a>
<a id="tocscloudcredentialobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "cloud_credential_info": {
    "type": "Invalid",
    "aws_config": {
      "access_key": "string",
      "secret_key": "string"
    },
    "azure_config": {
      "account_name": "string",
      "account_key": "string",
      "client_secret": "string",
      "client_id": "string",
      "tenant_id": "string",
      "subscription_id": "string"
    },
    "google_config": {
      "project_id": "string",
      "json_key": "string"
    }
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|cloud_credential_info|[CloudCredentialInfo](#schemacloudcredentialinfo)|false|none|none|

<h2 id="tocS_CloudCredentialUpdateRequest">CloudCredentialUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialupdaterequest"></a>
<a id="schema_CloudCredentialUpdateRequest"></a>
<a id="tocScloudcredentialupdaterequest"></a>
<a id="tocscloudcredentialupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "cloud_credential": {
    "type": "Invalid",
    "aws_config": {
      "access_key": "string",
      "secret_key": "string"
    },
    "azure_config": {
      "account_name": "string",
      "account_key": "string",
      "client_secret": "string",
      "client_id": "string",
      "tenant_id": "string",
      "subscription_id": "string"
    },
    "google_config": {
      "project_id": "string",
      "json_key": "string"
    }
  }
}

```

Define CloudCredentialUpdateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|cloud_credential|[CloudCredentialInfo](#schemacloudcredentialinfo)|false|none|none|

<h2 id="tocS_CloudCredentialUpdateResponse">CloudCredentialUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemacloudcredentialupdateresponse"></a>
<a id="schema_CloudCredentialUpdateResponse"></a>
<a id="tocScloudcredentialupdateresponse"></a>
<a id="tocscloudcredentialupdateresponse"></a>

```json
{}

```

Define CloudCredentialUpdateResponse struct

### Properties

*None*

<h2 id="tocS_ClusterCreateRequest">ClusterCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemaclustercreaterequest"></a>
<a id="schema_ClusterCreateRequest"></a>
<a id="tocSclustercreaterequest"></a>
<a id="tocsclustercreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "px_config": {
    "access_token": "string"
  },
  "kubeconfig": "string",
  "cloud_credential": "string"
}

```

Define ClusterCreateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|px_config|[PXConfig](#schemapxconfig)|false|none|none|
|kubeconfig|string|false|none|none|
|cloud_credential|string|false|none|none|

<h2 id="tocS_ClusterCreateResponse">ClusterCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclustercreateresponse"></a>
<a id="schema_ClusterCreateResponse"></a>
<a id="tocSclustercreateresponse"></a>
<a id="tocsclustercreateresponse"></a>

```json
{}

```

Define ClusterCreateResponse struct

### Properties

*None*

<h2 id="tocS_ClusterDeleteResponse">ClusterDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclusterdeleteresponse"></a>
<a id="schema_ClusterDeleteResponse"></a>
<a id="tocSclusterdeleteresponse"></a>
<a id="tocsclusterdeleteresponse"></a>

```json
{}

```

Define ClusterInspectResponse struct

### Properties

*None*

<h2 id="tocS_ClusterEnumerateResponse">ClusterEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclusterenumerateresponse"></a>
<a id="schema_ClusterEnumerateResponse"></a>
<a id="tocSclusterenumerateresponse"></a>
<a id="tocsclusterenumerateresponse"></a>

```json
{
  "clusters": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "clusterInfo": {
        "px_config": {
          "access_token": "string"
        },
        "kubeconfig": "string",
        "cloud_credential": "string",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "delete_backups": true,
        "delete_restores": true
      }
    }
  ]
}

```

Define ClusterEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|clusters|[[ClusterObject](#schemaclusterobject)]|false|none|none|

<h2 id="tocS_ClusterInfo">ClusterInfo</h2>
<!-- backwards compatibility -->
<a id="schemaclusterinfo"></a>
<a id="schema_ClusterInfo"></a>
<a id="tocSclusterinfo"></a>
<a id="tocsclusterinfo"></a>

```json
{
  "px_config": {
    "access_token": "string"
  },
  "kubeconfig": "string",
  "cloud_credential": "string",
  "status": {
    "status": "Invalid",
    "reason": "string"
  },
  "delete_backups": true,
  "delete_restores": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|px_config|[PXConfig](#schemapxconfig)|false|none|none|
|kubeconfig|string|false|none|none|
|cloud_credential|string|false|none|none|
|status|[ClusterInfoStatusInfo](#schemaclusterinfostatusinfo)|false|none|Message for maintaing status of the cluster.|
|delete_backups|boolean(boolean)|false|none|delete_backups will determine whether the backups<br>belong to given cluster needs to be deleted or not.|
|delete_restores|boolean(boolean)|false|none|delete_restores will determine whether the restore<br>belong to given cluster needs to be deleted or not.|

<h2 id="tocS_ClusterInfoStatusInfo">ClusterInfoStatusInfo</h2>
<!-- backwards compatibility -->
<a id="schemaclusterinfostatusinfo"></a>
<a id="schema_ClusterInfoStatusInfo"></a>
<a id="tocSclusterinfostatusinfo"></a>
<a id="tocsclusterinfostatusinfo"></a>

```json
{
  "status": "Invalid",
  "reason": "string"
}

```

Message for maintaing status of the cluster.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|[ClusterInfoStatusInfoStatus](#schemaclusterinfostatusinfostatus)|false|none|none|
|reason|string|false|none|none|

<h2 id="tocS_ClusterInfoStatusInfoStatus">ClusterInfoStatusInfoStatus</h2>
<!-- backwards compatibility -->
<a id="schemaclusterinfostatusinfostatus"></a>
<a id="schema_ClusterInfoStatusInfoStatus"></a>
<a id="tocSclusterinfostatusinfostatus"></a>
<a id="tocsclusterinfostatusinfostatus"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Online|
|*anonymous*|Offline|
|*anonymous*|DeletePending|

<h2 id="tocS_ClusterInspectResponse">ClusterInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclusterinspectresponse"></a>
<a id="schema_ClusterInspectResponse"></a>
<a id="tocSclusterinspectresponse"></a>
<a id="tocsclusterinspectresponse"></a>

```json
{
  "cluster": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "clusterInfo": {
      "px_config": {
        "access_token": "string"
      },
      "kubeconfig": "string",
      "cloud_credential": "string",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "delete_backups": true,
      "delete_restores": true
    }
  }
}

```

Define ClusterInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|cluster|[ClusterObject](#schemaclusterobject)|false|none|none|

<h2 id="tocS_ClusterObject">ClusterObject</h2>
<!-- backwards compatibility -->
<a id="schemaclusterobject"></a>
<a id="schema_ClusterObject"></a>
<a id="tocSclusterobject"></a>
<a id="tocsclusterobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "clusterInfo": {
    "px_config": {
      "access_token": "string"
    },
    "kubeconfig": "string",
    "cloud_credential": "string",
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "delete_backups": true,
    "delete_restores": true
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|clusterInfo|[ClusterInfo](#schemaclusterinfo)|false|none|none|

<h2 id="tocS_ClusterUpdateRequest">ClusterUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemaclusterupdaterequest"></a>
<a id="schema_ClusterUpdateRequest"></a>
<a id="tocSclusterupdaterequest"></a>
<a id="tocsclusterupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "px_config": {
    "access_token": "string"
  },
  "kubeconfig": "string",
  "cloud_credential": "string"
}

```

Define ClusterUpdateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|px_config|[PXConfig](#schemapxconfig)|false|none|none|
|kubeconfig|string|false|none|none|
|cloud_credential|string|false|none|none|

<h2 id="tocS_ClusterUpdateResponse">ClusterUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaclusterupdateresponse"></a>
<a id="schema_ClusterUpdateResponse"></a>
<a id="tocSclusterupdateresponse"></a>
<a id="tocsclusterupdateresponse"></a>

```json
{}

```

Define ClusterUpdateResponse struct

### Properties

*None*

<h2 id="tocS_CreateMetadata">CreateMetadata</h2>
<!-- backwards compatibility -->
<a id="schemacreatemetadata"></a>
<a id="schema_CreateMetadata"></a>
<a id="tocScreatemetadata"></a>
<a id="tocscreatemetadata"></a>

```json
{
  "name": "string",
  "org_id": "string",
  "owner": "string",
  "labels": {
    "property1": "string",
    "property2": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|org_id|string|false|none|none|
|owner|string|false|none|none|
|labels|object|false|none|none|
|» **additionalProperties**|string|false|none|none|

<h2 id="tocS_EnumerateOptions">EnumerateOptions</h2>
<!-- backwards compatibility -->
<a id="schemaenumerateoptions"></a>
<a id="schema_EnumerateOptions"></a>
<a id="tocSenumerateoptions"></a>
<a id="tocsenumerateoptions"></a>

```json
{
  "labels": {
    "property1": "string",
    "property2": "string"
  },
  "page_size": "string",
  "continuation_token": "string",
  "time_range": {
    "start_time": "2020-04-29T05:40:19Z",
    "end_time": "2020-04-29T05:40:19Z"
  },
  "name_filter": "string",
  "cluster_name_filter": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|labels|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|page_size|string(int64)|false|none|none|
|continuation_token|string|false|none|none|
|time_range|[TimeRange](#schematimerange)|false|none|none|
|name_filter|string|false|none|none|
|cluster_name_filter|string|false|none|none|

<h2 id="tocS_GoogleConfig">GoogleConfig</h2>
<!-- backwards compatibility -->
<a id="schemagoogleconfig"></a>
<a id="schema_GoogleConfig"></a>
<a id="tocSgoogleconfig"></a>
<a id="tocsgoogleconfig"></a>

```json
{
  "project_id": "string",
  "json_key": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|project_id|string|false|none|none|
|json_key|string|false|none|none|

<h2 id="tocS_HealthStatusResponse">HealthStatusResponse</h2>
<!-- backwards compatibility -->
<a id="schemahealthstatusresponse"></a>
<a id="schema_HealthStatusResponse"></a>
<a id="tocShealthstatusresponse"></a>
<a id="tocshealthstatusresponse"></a>

```json
{}

```

### Properties

*None*

<h2 id="tocS_LicenseActivateRequest">LicenseActivateRequest</h2>
<!-- backwards compatibility -->
<a id="schemalicenseactivaterequest"></a>
<a id="schema_LicenseActivateRequest"></a>
<a id="tocSlicenseactivaterequest"></a>
<a id="tocslicenseactivaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "activation_id": "string",
  "license_data": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|activation_id|string|false|none|none|
|license_data|string(byte)|false|none|none|

<h2 id="tocS_LicenseActivateResponse">LicenseActivateResponse</h2>
<!-- backwards compatibility -->
<a id="schemalicenseactivateresponse"></a>
<a id="schema_LicenseActivateResponse"></a>
<a id="tocSlicenseactivateresponse"></a>
<a id="tocslicenseactivateresponse"></a>

```json
{}

```

### Properties

*None*

<h2 id="tocS_LicenseInspectResponse">LicenseInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemalicenseinspectresponse"></a>
<a id="schema_LicenseInspectResponse"></a>
<a id="tocSlicenseinspectresponse"></a>
<a id="tocslicenseinspectresponse"></a>

```json
{
  "response_info": [
    {
      "name": "string",
      "count": "string",
      "expires": "2020-04-29T05:40:19Z",
      "starts": "2020-04-29T05:40:19Z"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|response_info|[[LicenseResponseInfo](#schemalicenseresponseinfo)]|false|none|none|

<h2 id="tocS_LicenseResponseInfo">LicenseResponseInfo</h2>
<!-- backwards compatibility -->
<a id="schemalicenseresponseinfo"></a>
<a id="schema_LicenseResponseInfo"></a>
<a id="tocSlicenseresponseinfo"></a>
<a id="tocslicenseresponseinfo"></a>

```json
{
  "name": "string",
  "count": "string",
  "expires": "2020-04-29T05:40:19Z",
  "starts": "2020-04-29T05:40:19Z"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|count|string(int64)|false|none|none|
|expires|string(date-time)|false|none|none|
|starts|string(date-time)|false|none|none|

<h2 id="tocS_Metadata">Metadata</h2>
<!-- backwards compatibility -->
<a id="schemametadata"></a>
<a id="schema_Metadata"></a>
<a id="tocSmetadata"></a>
<a id="tocsmetadata"></a>

```json
{
  "name": "string",
  "uid": "string",
  "owner": "string",
  "org_id": "string",
  "create_time": "2020-04-29T05:40:19Z",
  "last_update_time": "2020-04-29T05:40:19Z",
  "labels": {
    "property1": "string",
    "property2": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|uid|string|false|none|none|
|owner|string|false|none|none|
|org_id|string|false|none|none|
|create_time|string(date-time)|false|none|none|
|last_update_time|string(date-time)|false|none|none|
|labels|object|false|none|none|
|» **additionalProperties**|string|false|none|none|

<h2 id="tocS_OrganizationCreateRequest">OrganizationCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationcreaterequest"></a>
<a id="schema_OrganizationCreateRequest"></a>
<a id="tocSorganizationcreaterequest"></a>
<a id="tocsorganizationcreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  }
}

```

Define OrganizationCreateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|

<h2 id="tocS_OrganizationCreateResponse">OrganizationCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationcreateresponse"></a>
<a id="schema_OrganizationCreateResponse"></a>
<a id="tocSorganizationcreateresponse"></a>
<a id="tocsorganizationcreateresponse"></a>

```json
{}

```

Define OrganizationCreateResponse struct

### Properties

*None*

<h2 id="tocS_OrganizationEnumerateResponse">OrganizationEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationenumerateresponse"></a>
<a id="schema_OrganizationEnumerateResponse"></a>
<a id="tocSorganizationenumerateresponse"></a>
<a id="tocsorganizationenumerateresponse"></a>

```json
{
  "organizations": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      }
    }
  ]
}

```

Define OrganizationEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|organizations|[[OrganizationObject](#schemaorganizationobject)]|false|none|none|

<h2 id="tocS_OrganizationInspectResponse">OrganizationInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationinspectresponse"></a>
<a id="schema_OrganizationInspectResponse"></a>
<a id="tocSorganizationinspectresponse"></a>
<a id="tocsorganizationinspectresponse"></a>

```json
{
  "organization": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    }
  }
}

```

Define OrganizationInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|organization|[OrganizationObject](#schemaorganizationobject)|false|none|none|

<h2 id="tocS_OrganizationObject">OrganizationObject</h2>
<!-- backwards compatibility -->
<a id="schemaorganizationobject"></a>
<a id="schema_OrganizationObject"></a>
<a id="tocSorganizationobject"></a>
<a id="tocsorganizationobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|

<h2 id="tocS_PXConfig">PXConfig</h2>
<!-- backwards compatibility -->
<a id="schemapxconfig"></a>
<a id="schema_PXConfig"></a>
<a id="tocSpxconfig"></a>
<a id="tocspxconfig"></a>

```json
{
  "access_token": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|access_token|string|false|none|none|

<h2 id="tocS_ReplacePolicyType">ReplacePolicyType</h2>
<!-- backwards compatibility -->
<a id="schemareplacepolicytype"></a>
<a id="schema_ReplacePolicyType"></a>
<a id="tocSreplacepolicytype"></a>
<a id="tocsreplacepolicytype"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Retain|
|*anonymous*|Delete|

<h2 id="tocS_RestoreCreateRequest">RestoreCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemarestorecreaterequest"></a>
<a id="schema_RestoreCreateRequest"></a>
<a id="tocSrestorecreaterequest"></a>
<a id="tocsrestorecreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "backup": "string",
  "cluster": "string",
  "namespace_mapping": {
    "property1": "string",
    "property2": "string"
  },
  "replace_policy": "Invalid"
}

```

Define RestoreCreateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|backup|string|false|none|none|
|cluster|string|false|none|none|
|namespace_mapping|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|replace_policy|[ReplacePolicyType](#schemareplacepolicytype)|false|none|none|

<h2 id="tocS_RestoreCreateResponse">RestoreCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemarestorecreateresponse"></a>
<a id="schema_RestoreCreateResponse"></a>
<a id="tocSrestorecreateresponse"></a>
<a id="tocsrestorecreateresponse"></a>

```json
{}

```

Define RestoreCreateResponse struct

### Properties

*None*

<h2 id="tocS_RestoreDeleteResponse">RestoreDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemarestoredeleteresponse"></a>
<a id="schema_RestoreDeleteResponse"></a>
<a id="tocSrestoredeleteresponse"></a>
<a id="tocsrestoredeleteresponse"></a>

```json
{}

```

Define RestoreDeleteResponse struct

### Properties

*None*

<h2 id="tocS_RestoreEnumerateResponse">RestoreEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemarestoreenumerateresponse"></a>
<a id="schema_RestoreEnumerateResponse"></a>
<a id="tocSrestoreenumerateresponse"></a>
<a id="tocsrestoreenumerateresponse"></a>

```json
{
  "restores": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "restore_info": {
        "backup": "string",
        "backup_location": "string",
        "label_selectors": {
          "property1": "string",
          "property2": "string"
        },
        "namespace_mapping": {
          "property1": "string",
          "property2": "string"
        },
        "replace_policy": "Invalid",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "resources": [
          {
            "name": "string",
            "namespace": "string",
            "group": "string",
            "kind": "string",
            "version": "string",
            "status": {
              "status": "Invalid",
              "reason": "string"
            }
          }
        ],
        "volumes": [
          {
            "pvc": "string",
            "source_namespace": "string",
            "source_volume": "string",
            "restore_volume": "string",
            "status": {
              "status": "Invalid",
              "reason": "string"
            },
            "driver_name": "string",
            "zones": [
              "string"
            ],
            "options": {
              "property1": "string",
              "property2": "string"
            }
          }
        ],
        "cluster": "string"
      }
    }
  ],
  "continuation_token": "string"
}

```

Define RestoreEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|restores|[[RestoreObject](#schemarestoreobject)]|false|none|[Message for Restore object which will be stored in Datastore.]|
|continuation_token|string|false|none|none|

<h2 id="tocS_RestoreInfo">RestoreInfo</h2>
<!-- backwards compatibility -->
<a id="schemarestoreinfo"></a>
<a id="schema_RestoreInfo"></a>
<a id="tocSrestoreinfo"></a>
<a id="tocsrestoreinfo"></a>

```json
{
  "backup": "string",
  "backup_location": "string",
  "label_selectors": {
    "property1": "string",
    "property2": "string"
  },
  "namespace_mapping": {
    "property1": "string",
    "property2": "string"
  },
  "replace_policy": "Invalid",
  "status": {
    "status": "Invalid",
    "reason": "string"
  },
  "resources": [
    {
      "name": "string",
      "namespace": "string",
      "group": "string",
      "kind": "string",
      "version": "string",
      "status": {
        "status": "Invalid",
        "reason": "string"
      }
    }
  ],
  "volumes": [
    {
      "pvc": "string",
      "source_namespace": "string",
      "source_volume": "string",
      "restore_volume": "string",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "driver_name": "string",
      "zones": [
        "string"
      ],
      "options": {
        "property1": "string",
        "property2": "string"
      }
    }
  ],
  "cluster": "string"
}

```

Message for restore info

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|backup|string|false|none|none|
|backup_location|string|false|none|none|
|label_selectors|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|namespace_mapping|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|replace_policy|[ReplacePolicyType](#schemareplacepolicytype)|false|none|none|
|status|[RestoreInfoStatusInfo](#schemarestoreinfostatusinfo)|false|none|Message for maintaing status of the object.|
|resources|[[RestoreInfoResource](#schemarestoreinforesource)]|false|none|none|
|volumes|[[RestoreInfoVolume](#schemarestoreinfovolume)]|false|none|none|
|cluster|string|false|none|none|

<h2 id="tocS_RestoreInfoResource">RestoreInfoResource</h2>
<!-- backwards compatibility -->
<a id="schemarestoreinforesource"></a>
<a id="schema_RestoreInfoResource"></a>
<a id="tocSrestoreinforesource"></a>
<a id="tocsrestoreinforesource"></a>

```json
{
  "name": "string",
  "namespace": "string",
  "group": "string",
  "kind": "string",
  "version": "string",
  "status": {
    "status": "Invalid",
    "reason": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|
|namespace|string|false|none|none|
|group|string|false|none|none|
|kind|string|false|none|none|
|version|string|false|none|none|
|status|[RestoreInfoStatusInfo](#schemarestoreinfostatusinfo)|false|none|Message for maintaing status of the object.|

<h2 id="tocS_RestoreInfoStatusInfo">RestoreInfoStatusInfo</h2>
<!-- backwards compatibility -->
<a id="schemarestoreinfostatusinfo"></a>
<a id="schema_RestoreInfoStatusInfo"></a>
<a id="tocSrestoreinfostatusinfo"></a>
<a id="tocsrestoreinfostatusinfo"></a>

```json
{
  "status": "Invalid",
  "reason": "string"
}

```

Message for maintaing status of the object.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|status|[RestoreInfoStatusInfoStatus](#schemarestoreinfostatusinfostatus)|false|none|none|
|reason|string|false|none|none|

<h2 id="tocS_RestoreInfoStatusInfoStatus">RestoreInfoStatusInfoStatus</h2>
<!-- backwards compatibility -->
<a id="schemarestoreinfostatusinfostatus"></a>
<a id="schema_RestoreInfoStatusInfoStatus"></a>
<a id="tocSrestoreinfostatusinfostatus"></a>
<a id="tocsrestoreinfostatusinfostatus"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|Pending|
|*anonymous*|InProgress|
|*anonymous*|Aborted|
|*anonymous*|Failed|
|*anonymous*|Deleting|
|*anonymous*|Success|
|*anonymous*|Retained|
|*anonymous*|PartialSuccess|

<h2 id="tocS_RestoreInfoVolume">RestoreInfoVolume</h2>
<!-- backwards compatibility -->
<a id="schemarestoreinfovolume"></a>
<a id="schema_RestoreInfoVolume"></a>
<a id="tocSrestoreinfovolume"></a>
<a id="tocsrestoreinfovolume"></a>

```json
{
  "pvc": "string",
  "source_namespace": "string",
  "source_volume": "string",
  "restore_volume": "string",
  "status": {
    "status": "Invalid",
    "reason": "string"
  },
  "driver_name": "string",
  "zones": [
    "string"
  ],
  "options": {
    "property1": "string",
    "property2": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|pvc|string|false|none|none|
|source_namespace|string|false|none|none|
|source_volume|string|false|none|none|
|restore_volume|string|false|none|none|
|status|[RestoreInfoStatusInfo](#schemarestoreinfostatusinfo)|false|none|Message for maintaing status of the object.|
|driver_name|string|false|none|none|
|zones|[string]|false|none|none|
|options|object|false|none|none|
|» **additionalProperties**|string|false|none|none|

<h2 id="tocS_RestoreInspectResponse">RestoreInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemarestoreinspectresponse"></a>
<a id="schema_RestoreInspectResponse"></a>
<a id="tocSrestoreinspectresponse"></a>
<a id="tocsrestoreinspectresponse"></a>

```json
{
  "restore": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "restore_info": {
      "backup": "string",
      "backup_location": "string",
      "label_selectors": {
        "property1": "string",
        "property2": "string"
      },
      "namespace_mapping": {
        "property1": "string",
        "property2": "string"
      },
      "replace_policy": "Invalid",
      "status": {
        "status": "Invalid",
        "reason": "string"
      },
      "resources": [
        {
          "name": "string",
          "namespace": "string",
          "group": "string",
          "kind": "string",
          "version": "string",
          "status": {
            "status": "Invalid",
            "reason": "string"
          }
        }
      ],
      "volumes": [
        {
          "pvc": "string",
          "source_namespace": "string",
          "source_volume": "string",
          "restore_volume": "string",
          "status": {
            "status": "Invalid",
            "reason": "string"
          },
          "driver_name": "string",
          "zones": [
            "string"
          ],
          "options": {
            "property1": "string",
            "property2": "string"
          }
        }
      ],
      "cluster": "string"
    }
  }
}

```

Define RestoreInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|restore|[RestoreObject](#schemarestoreobject)|false|none|Message for Restore object which will be stored in Datastore.|

<h2 id="tocS_RestoreObject">RestoreObject</h2>
<!-- backwards compatibility -->
<a id="schemarestoreobject"></a>
<a id="schema_RestoreObject"></a>
<a id="tocSrestoreobject"></a>
<a id="tocsrestoreobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "restore_info": {
    "backup": "string",
    "backup_location": "string",
    "label_selectors": {
      "property1": "string",
      "property2": "string"
    },
    "namespace_mapping": {
      "property1": "string",
      "property2": "string"
    },
    "replace_policy": "Invalid",
    "status": {
      "status": "Invalid",
      "reason": "string"
    },
    "resources": [
      {
        "name": "string",
        "namespace": "string",
        "group": "string",
        "kind": "string",
        "version": "string",
        "status": {
          "status": "Invalid",
          "reason": "string"
        }
      }
    ],
    "volumes": [
      {
        "pvc": "string",
        "source_namespace": "string",
        "source_volume": "string",
        "restore_volume": "string",
        "status": {
          "status": "Invalid",
          "reason": "string"
        },
        "driver_name": "string",
        "zones": [
          "string"
        ],
        "options": {
          "property1": "string",
          "property2": "string"
        }
      }
    ],
    "cluster": "string"
  }
}

```

Message for Restore object which will be stored in Datastore.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|restore_info|[RestoreInfo](#schemarestoreinfo)|false|none|none|

<h2 id="tocS_RestoreUpdateRequest">RestoreUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemarestoreupdaterequest"></a>
<a id="schema_RestoreUpdateRequest"></a>
<a id="tocSrestoreupdaterequest"></a>
<a id="tocsrestoreupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  }
}

```

Define RestoreUpdateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|

<h2 id="tocS_RestoreUpdateResponse">RestoreUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemarestoreupdateresponse"></a>
<a id="schema_RestoreUpdateResponse"></a>
<a id="tocSrestoreupdateresponse"></a>
<a id="tocsrestoreupdateresponse"></a>

```json
{}

```

Define RestoreUpdateResponse struct

### Properties

*None*

<h2 id="tocS_RuleCreateRequest">RuleCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemarulecreaterequest"></a>
<a id="schema_RuleCreateRequest"></a>
<a id="tocSrulecreaterequest"></a>
<a id="tocsrulecreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "rules_info": {
    "rules": [
      {
        "pod_selector": {
          "property1": "string",
          "property2": "string"
        },
        "actions": [
          {
            "background": true,
            "run_in_single_pod": true,
            "value": "string"
          }
        ]
      }
    ]
  }
}

```

Request message for creating rules

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|rules_info|[RulesInfo](#schemarulesinfo)|false|none|none|

<h2 id="tocS_RuleCreateResponse">RuleCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemarulecreateresponse"></a>
<a id="schema_RuleCreateResponse"></a>
<a id="tocSrulecreateresponse"></a>
<a id="tocsrulecreateresponse"></a>

```json
{}

```

### Properties

*None*

<h2 id="tocS_RuleDeleteResponse">RuleDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemaruledeleteresponse"></a>
<a id="schema_RuleDeleteResponse"></a>
<a id="tocSruledeleteresponse"></a>
<a id="tocsruledeleteresponse"></a>

```json
{}

```

Define RuleDeleteResponse struct

### Properties

*None*

<h2 id="tocS_RuleEnumerateResponse">RuleEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaruleenumerateresponse"></a>
<a id="schema_RuleEnumerateResponse"></a>
<a id="tocSruleenumerateresponse"></a>
<a id="tocsruleenumerateresponse"></a>

```json
{
  "rules": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "rules_info": {
        "rules": [
          {
            "pod_selector": {
              "property1": "string",
              "property2": "string"
            },
            "actions": [
              {
                "background": true,
                "run_in_single_pod": true,
                "value": "string"
              }
            ]
          }
        ]
      }
    }
  ]
}

```

Define RuleEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|rules|[[RuleObject](#schemaruleobject)]|false|none|none|

<h2 id="tocS_RuleInspectResponse">RuleInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemaruleinspectresponse"></a>
<a id="schema_RuleInspectResponse"></a>
<a id="tocSruleinspectresponse"></a>
<a id="tocsruleinspectresponse"></a>

```json
{
  "rule": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "rules_info": {
      "rules": [
        {
          "pod_selector": {
            "property1": "string",
            "property2": "string"
          },
          "actions": [
            {
              "background": true,
              "run_in_single_pod": true,
              "value": "string"
            }
          ]
        }
      ]
    }
  }
}

```

Define RuleInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|rule|[RuleObject](#schemaruleobject)|false|none|none|

<h2 id="tocS_RuleObject">RuleObject</h2>
<!-- backwards compatibility -->
<a id="schemaruleobject"></a>
<a id="schema_RuleObject"></a>
<a id="tocSruleobject"></a>
<a id="tocsruleobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "rules_info": {
    "rules": [
      {
        "pod_selector": {
          "property1": "string",
          "property2": "string"
        },
        "actions": [
          {
            "background": true,
            "run_in_single_pod": true,
            "value": "string"
          }
        ]
      }
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|rules_info|[RulesInfo](#schemarulesinfo)|false|none|none|

<h2 id="tocS_RuleUpdateRequest">RuleUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemaruleupdaterequest"></a>
<a id="schema_RuleUpdateRequest"></a>
<a id="tocSruleupdaterequest"></a>
<a id="tocsruleupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "rules_info": {
    "rules": [
      {
        "pod_selector": {
          "property1": "string",
          "property2": "string"
        },
        "actions": [
          {
            "background": true,
            "run_in_single_pod": true,
            "value": "string"
          }
        ]
      }
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|rules_info|[RulesInfo](#schemarulesinfo)|false|none|none|

<h2 id="tocS_RuleUpdateResponse">RuleUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaruleupdateresponse"></a>
<a id="schema_RuleUpdateResponse"></a>
<a id="tocSruleupdateresponse"></a>
<a id="tocsruleupdateresponse"></a>

```json
{}

```

Define RuleUpdateResponse struct

### Properties

*None*

<h2 id="tocS_RulesInfo">RulesInfo</h2>
<!-- backwards compatibility -->
<a id="schemarulesinfo"></a>
<a id="schema_RulesInfo"></a>
<a id="tocSrulesinfo"></a>
<a id="tocsrulesinfo"></a>

```json
{
  "rules": [
    {
      "pod_selector": {
        "property1": "string",
        "property2": "string"
      },
      "actions": [
        {
          "background": true,
          "run_in_single_pod": true,
          "value": "string"
        }
      ]
    }
  ]
}

```

Message for passing pre and post exec rules for backup

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|rules|[[RulesInfoRuleItem](#schemarulesinforuleitem)]|false|none|none|

<h2 id="tocS_RulesInfoRuleAction">RulesInfoRuleAction</h2>
<!-- backwards compatibility -->
<a id="schemarulesinforuleaction"></a>
<a id="schema_RulesInfoRuleAction"></a>
<a id="tocSrulesinforuleaction"></a>
<a id="tocsrulesinforuleaction"></a>

```json
{
  "background": true,
  "run_in_single_pod": true,
  "value": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|background|boolean(boolean)|false|none|none|
|run_in_single_pod|boolean(boolean)|false|none|none|
|value|string|false|none|none|

<h2 id="tocS_RulesInfoRuleItem">RulesInfoRuleItem</h2>
<!-- backwards compatibility -->
<a id="schemarulesinforuleitem"></a>
<a id="schema_RulesInfoRuleItem"></a>
<a id="tocSrulesinforuleitem"></a>
<a id="tocsrulesinforuleitem"></a>

```json
{
  "pod_selector": {
    "property1": "string",
    "property2": "string"
  },
  "actions": [
    {
      "background": true,
      "run_in_single_pod": true,
      "value": "string"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|pod_selector|object|false|none|none|
|» **additionalProperties**|string|false|none|none|
|actions|[[RulesInfoRuleAction](#schemarulesinforuleaction)]|false|none|none|

<h2 id="tocS_S3Config">S3Config</h2>
<!-- backwards compatibility -->
<a id="schemas3config"></a>
<a id="schema_S3Config"></a>
<a id="tocSs3config"></a>
<a id="tocss3config"></a>

```json
{
  "endpoint": "string",
  "region": "string",
  "disable_ssl": true,
  "disable_path_style": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|endpoint|string|false|none|none|
|region|string|false|none|none|
|disable_ssl|boolean(boolean)|false|none|none|
|disable_path_style|boolean(boolean)|false|none|none|

<h2 id="tocS_SchedulePolicyCreateRequest">SchedulePolicyCreateRequest</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicycreaterequest"></a>
<a id="schema_SchedulePolicyCreateRequest"></a>
<a id="tocSschedulepolicycreaterequest"></a>
<a id="tocsschedulepolicycreaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": {
    "interval": {
      "minutes": "string",
      "retain": "string"
    },
    "daily": {
      "time": "string",
      "retain": "string"
    },
    "weekly": {
      "day": "string",
      "time": "string",
      "retain": "string"
    },
    "monthly": {
      "date": "string",
      "time": "string",
      "retain": "string"
    },
    "backup_schedule": [
      "string"
    ]
  }
}

```

Define SchedulePolicyCreateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|schedule_policy|[SchedulePolicyInfo](#schemaschedulepolicyinfo)|false|none|none|

<h2 id="tocS_SchedulePolicyCreateResponse">SchedulePolicyCreateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicycreateresponse"></a>
<a id="schema_SchedulePolicyCreateResponse"></a>
<a id="tocSschedulepolicycreateresponse"></a>
<a id="tocsschedulepolicycreateresponse"></a>

```json
{}

```

Define SchedulePolicyCreateResponse struct

### Properties

*None*

<h2 id="tocS_SchedulePolicyDeleteResponse">SchedulePolicyDeleteResponse</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicydeleteresponse"></a>
<a id="schema_SchedulePolicyDeleteResponse"></a>
<a id="tocSschedulepolicydeleteresponse"></a>
<a id="tocsschedulepolicydeleteresponse"></a>

```json
{}

```

Define SchedulePolicyDeleteResponse struct

### Properties

*None*

<h2 id="tocS_SchedulePolicyEnumerateResponse">SchedulePolicyEnumerateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyenumerateresponse"></a>
<a id="schema_SchedulePolicyEnumerateResponse"></a>
<a id="tocSschedulepolicyenumerateresponse"></a>
<a id="tocsschedulepolicyenumerateresponse"></a>

```json
{
  "schedule_policies": [
    {
      "metadata": {
        "name": "string",
        "uid": "string",
        "owner": "string",
        "org_id": "string",
        "create_time": "2020-04-29T05:40:19Z",
        "last_update_time": "2020-04-29T05:40:19Z",
        "labels": {
          "property1": "string",
          "property2": "string"
        }
      },
      "schedule_policy_info": {
        "interval": {
          "minutes": "string",
          "retain": "string"
        },
        "daily": {
          "time": "string",
          "retain": "string"
        },
        "weekly": {
          "day": "string",
          "time": "string",
          "retain": "string"
        },
        "monthly": {
          "date": "string",
          "time": "string",
          "retain": "string"
        },
        "backup_schedule": [
          "string"
        ]
      }
    }
  ]
}

```

Define SchedulePolicyEnumerateResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|schedule_policies|[[SchedulePolicyObject](#schemaschedulepolicyobject)]|false|none|none|

<h2 id="tocS_SchedulePolicyInfo">SchedulePolicyInfo</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyinfo"></a>
<a id="schema_SchedulePolicyInfo"></a>
<a id="tocSschedulepolicyinfo"></a>
<a id="tocsschedulepolicyinfo"></a>

```json
{
  "interval": {
    "minutes": "string",
    "retain": "string"
  },
  "daily": {
    "time": "string",
    "retain": "string"
  },
  "weekly": {
    "day": "string",
    "time": "string",
    "retain": "string"
  },
  "monthly": {
    "date": "string",
    "time": "string",
    "retain": "string"
  },
  "backup_schedule": [
    "string"
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|interval|[SchedulePolicyInfoIntervalPolicy](#schemaschedulepolicyinfointervalpolicy)|false|none|none|
|daily|[SchedulePolicyInfoDailyPolicy](#schemaschedulepolicyinfodailypolicy)|false|none|none|
|weekly|[SchedulePolicyInfoWeeklyPolicy](#schemaschedulepolicyinfoweeklypolicy)|false|none|none|
|monthly|[SchedulePolicyInfoMonthlyPolicy](#schemaschedulepolicyinfomonthlypolicy)|false|none|none|
|backup_schedule|[string]|false|none|list of backup schedule object that uses this schedule policy.|

<h2 id="tocS_SchedulePolicyInfoDailyPolicy">SchedulePolicyInfoDailyPolicy</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyinfodailypolicy"></a>
<a id="schema_SchedulePolicyInfoDailyPolicy"></a>
<a id="tocSschedulepolicyinfodailypolicy"></a>
<a id="tocsschedulepolicyinfodailypolicy"></a>

```json
{
  "time": "string",
  "retain": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|time|string|false|none|Time, when the policy should be triggered. Expected format is<br>time.Kitchen eg 12:04PM or 12:04pm.|
|retain|string(int64)|false|none|Number of objects to retain for daily policy, default value is 10.|

<h2 id="tocS_SchedulePolicyInfoIntervalPolicy">SchedulePolicyInfoIntervalPolicy</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyinfointervalpolicy"></a>
<a id="schema_SchedulePolicyInfoIntervalPolicy"></a>
<a id="tocSschedulepolicyinfointervalpolicy"></a>
<a id="tocsschedulepolicyinfointervalpolicy"></a>

```json
{
  "minutes": "string",
  "retain": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|minutes|string(int64)|false|none|Interval in minutes at which an action should be triggered.|
|retain|string(int64)|false|none|Number of objects to retain for interval policy, default value is 10.|

<h2 id="tocS_SchedulePolicyInfoMonthlyPolicy">SchedulePolicyInfoMonthlyPolicy</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyinfomonthlypolicy"></a>
<a id="schema_SchedulePolicyInfoMonthlyPolicy"></a>
<a id="tocSschedulepolicyinfomonthlypolicy"></a>
<a id="tocsschedulepolicyinfomonthlypolicy"></a>

```json
{
  "date": "string",
  "time": "string",
  "retain": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|date|string(int64)|false|none|Date of the month when the policy should be triggered. If a given<br>date<br>doesn't exist in a month it'll rollover to the next date of the<br>month.<br>For example if 31 is specified, it'll trigger on either 1st or 2nd<br>March<br>depending on if it is a leap year.|
|time|string|false|none|Time, when the policy should be triggered. Expected format is<br>time.Kitchen eg 12:04PM or 12:04pm.|
|retain|string(int64)|false|none|Number of objects to retain for monthly policy, default value is 10.|

<h2 id="tocS_SchedulePolicyInfoWeeklyPolicy">SchedulePolicyInfoWeeklyPolicy</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyinfoweeklypolicy"></a>
<a id="schema_SchedulePolicyInfoWeeklyPolicy"></a>
<a id="tocSschedulepolicyinfoweeklypolicy"></a>
<a id="tocsschedulepolicyinfoweeklypolicy"></a>

```json
{
  "day": "string",
  "time": "string",
  "retain": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|day|string|false|none|none|
|time|string|false|none|Time, when the policy should be triggered. Expected format is<br>time.Kitchen eg 12:04PM or 12:04pm.|
|retain|string(int64)|false|none|Number of objects to retain for weekly policy, default value is 10.|

<h2 id="tocS_SchedulePolicyInspectResponse">SchedulePolicyInspectResponse</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyinspectresponse"></a>
<a id="schema_SchedulePolicyInspectResponse"></a>
<a id="tocSschedulepolicyinspectresponse"></a>
<a id="tocsschedulepolicyinspectresponse"></a>

```json
{
  "schedule_policy": {
    "metadata": {
      "name": "string",
      "uid": "string",
      "owner": "string",
      "org_id": "string",
      "create_time": "2020-04-29T05:40:19Z",
      "last_update_time": "2020-04-29T05:40:19Z",
      "labels": {
        "property1": "string",
        "property2": "string"
      }
    },
    "schedule_policy_info": {
      "interval": {
        "minutes": "string",
        "retain": "string"
      },
      "daily": {
        "time": "string",
        "retain": "string"
      },
      "weekly": {
        "day": "string",
        "time": "string",
        "retain": "string"
      },
      "monthly": {
        "date": "string",
        "time": "string",
        "retain": "string"
      },
      "backup_schedule": [
        "string"
      ]
    }
  }
}

```

Define SchedulePolicyInspectResponse struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|schedule_policy|[SchedulePolicyObject](#schemaschedulepolicyobject)|false|none|none|

<h2 id="tocS_SchedulePolicyObject">SchedulePolicyObject</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyobject"></a>
<a id="schema_SchedulePolicyObject"></a>
<a id="tocSschedulepolicyobject"></a>
<a id="tocsschedulepolicyobject"></a>

```json
{
  "metadata": {
    "name": "string",
    "uid": "string",
    "owner": "string",
    "org_id": "string",
    "create_time": "2020-04-29T05:40:19Z",
    "last_update_time": "2020-04-29T05:40:19Z",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy_info": {
    "interval": {
      "minutes": "string",
      "retain": "string"
    },
    "daily": {
      "time": "string",
      "retain": "string"
    },
    "weekly": {
      "day": "string",
      "time": "string",
      "retain": "string"
    },
    "monthly": {
      "date": "string",
      "time": "string",
      "retain": "string"
    },
    "backup_schedule": [
      "string"
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[Metadata](#schemametadata)|false|none|none|
|schedule_policy_info|[SchedulePolicyInfo](#schemaschedulepolicyinfo)|false|none|none|

<h2 id="tocS_SchedulePolicyUpdateRequest">SchedulePolicyUpdateRequest</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyupdaterequest"></a>
<a id="schema_SchedulePolicyUpdateRequest"></a>
<a id="tocSschedulepolicyupdaterequest"></a>
<a id="tocsschedulepolicyupdaterequest"></a>

```json
{
  "metadata": {
    "name": "string",
    "org_id": "string",
    "owner": "string",
    "labels": {
      "property1": "string",
      "property2": "string"
    }
  },
  "schedule_policy": {
    "interval": {
      "minutes": "string",
      "retain": "string"
    },
    "daily": {
      "time": "string",
      "retain": "string"
    },
    "weekly": {
      "day": "string",
      "time": "string",
      "retain": "string"
    },
    "monthly": {
      "date": "string",
      "time": "string",
      "retain": "string"
    },
    "backup_schedule": [
      "string"
    ]
  }
}

```

Define SchedulePolicyUpdateRequest struct

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|metadata|[CreateMetadata](#schemacreatemetadata)|false|none|none|
|schedule_policy|[SchedulePolicyInfo](#schemaschedulepolicyinfo)|false|none|none|

<h2 id="tocS_SchedulePolicyUpdateResponse">SchedulePolicyUpdateResponse</h2>
<!-- backwards compatibility -->
<a id="schemaschedulepolicyupdateresponse"></a>
<a id="schema_SchedulePolicyUpdateResponse"></a>
<a id="tocSschedulepolicyupdateresponse"></a>
<a id="tocsschedulepolicyupdateresponse"></a>

```json
{}

```

Define SchedulePolicyUpdateResponse struct

### Properties

*None*

<h2 id="tocS_SuspendedBySource">SuspendedBySource</h2>
<!-- backwards compatibility -->
<a id="schemasuspendedbysource"></a>
<a id="schema_SuspendedBySource"></a>
<a id="tocSsuspendedbysource"></a>
<a id="tocssuspendedbysource"></a>

```json
"Invalid"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Invalid|
|*anonymous*|User|
|*anonymous*|LicenseCheck|

<h2 id="tocS_TimeRange">TimeRange</h2>
<!-- backwards compatibility -->
<a id="schematimerange"></a>
<a id="schema_TimeRange"></a>
<a id="tocStimerange"></a>
<a id="tocstimerange"></a>

```json
{
  "start_time": "2020-04-29T05:40:19Z",
  "end_time": "2020-04-29T05:40:19Z"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|start_time|string(date-time)|false|none|none|
|end_time|string(date-time)|false|none|none|

<h2 id="tocS_VersionGetResponse">VersionGetResponse</h2>
<!-- backwards compatibility -->
<a id="schemaversiongetresponse"></a>
<a id="schema_VersionGetResponse"></a>
<a id="tocSversiongetresponse"></a>
<a id="tocsversiongetresponse"></a>

```json
{
  "version": {
    "major": "string",
    "minor": "string",
    "patch": "string",
    "git_commit": "string",
    "build_date": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|version|[VersionInfo](#schemaversioninfo)|false|none|none|

<h2 id="tocS_VersionInfo">VersionInfo</h2>
<!-- backwards compatibility -->
<a id="schemaversioninfo"></a>
<a id="schema_VersionInfo"></a>
<a id="tocSversioninfo"></a>
<a id="tocsversioninfo"></a>

```json
{
  "major": "string",
  "minor": "string",
  "patch": "string",
  "git_commit": "string",
  "build_date": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|major|string|false|none|none|
|minor|string|false|none|none|
|patch|string|false|none|none|
|git_commit|string|false|none|none|
|build_date|string|false|none|none|

<h2 id="tocS_protobufAny">protobufAny</h2>
<!-- backwards compatibility -->
<a id="schemaprotobufany"></a>
<a id="schema_protobufAny"></a>
<a id="tocSprotobufany"></a>
<a id="tocsprotobufany"></a>

```json
{
  "type_url": "string",
  "value": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type_url|string|false|none|none|
|value|string(byte)|false|none|none|

<h2 id="tocS_runtimeError">runtimeError</h2>
<!-- backwards compatibility -->
<a id="schemaruntimeerror"></a>
<a id="schema_runtimeError"></a>
<a id="tocSruntimeerror"></a>
<a id="tocsruntimeerror"></a>

```json
{
  "error": "string",
  "code": 0,
  "message": "string",
  "details": [
    {
      "type_url": "string",
      "value": "string"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|error|string|false|none|none|
|code|integer(int32)|false|none|none|
|message|string|false|none|none|
|details|[[protobufAny](#schemaprotobufany)]|false|none|none|

