---
title: List Investigations API
description: Use this API to create calls related to get Investigations collection.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
- must-keep
ms.topic: reference
ms.subservice: reference
ms.custom: api
search.appverid: met150
ms.date: 12/18/2020
---

# List Investigations API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Retrieves a collection of [Investigations](investigation.md).

Supports [OData V4 queries](https://www.odata.org/documentation/).

The OData's `$filter` query is supported on: `startTime`, `id`, `state`, `machineId`, and `triggeringAlertId` properties.
<br>```$stop``` with max value of 10,000 
<br>```$skip```

See examples at [OData queries with Microsoft Defender for Endpoint](exposed-apis-odata-samples.md)

## Limitations

1. Maximum page size is 10,000.
2. Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md).

|Permission type|Permission|Permission display name|
|:---|:---|:---|
|Application|Alert.Read.All|`Read all alerts` |
|Application|Alert.ReadWrite.All|`Read and write all alerts` |
|Delegated (work or school account)|Alert.Read|`Read alerts` |
|Delegated (work or school account)|Alert.ReadWrite|`Read and write alerts` |

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have at least the following role permission: `View Data`. For more information, see [Create and manage roles](../user-roles.md) for more information.

## HTTP request

```http
GET https://api.securitycenter.microsoft.com/api/investigations
```

## Request headers

|Name|Type|Description|
|:---|:---|:---|
|Authorization|String|Bearer {token}. **Required**.|

## Request body

Empty

## Response

If successful, this method returns 200, Ok response code with a collection of [Investigations](investigation.md) entities.

## Example

### Request example

Here's an example of a request to get all investigations:

```http
GET https://api.securitycenter.microsoft.com/api/investigations
```

### Response example

Here's an example of the response:

```json
{
    "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Investigations",
    "value": [
        {
            "id": "63017",
            "startTime": "2020-01-06T14:11:34Z",
            "endTime": null,
            "state": "Running",
            "cancelledBy": null,
            "statusDetails": null,
            "machineId": "a69a22debe5f274d8765ea3c368d00762e057b30",
            "computerDnsName": "desktop-gtrcon0",
            "triggeringAlertId": "da637139166940871892_-598649278"
        }
        ...
    ]
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
