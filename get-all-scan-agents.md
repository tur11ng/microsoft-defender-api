---
title: Get all scan agents
description: Learn how to use the Get all scan agents API
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
ms.date: 12/14/2022
---

# Get all scan agents

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

> Want to experience Microsoft Defender Vulnerability Management? Find out how to [sign up for a free trial](/defender-vulnerability-management/get-defender-vulnerability-management).

[!Include[Prerelease information](../../includes/prerelease.md)]

[!Include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!Include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Retrieves a list of all scan agents.

## Limitations

1. Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md).

Permission type|Permission|Permission display name
:---|:---|:---
Application|Machine.Read.All| Read all scan information.
Delegated (work or school account)|Machine.Read.All|Read all scan information.

When obtaining a token using user credentials, to view data, the user needs to have at least the following role permission: `ViewData` or `TvmViewData` (See [Create and manage roles](../user-roles.md))

## HTTP request

```http
GET /api/DeviceAuthenticatedScanAgents
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization|String|Bearer {token}. **Required**.

## Request body

Empty

## Response

If successful, this method returns 200 - OK response code with a list of authenticated scan agents.

## Example

### Request example

Here's an example of the request.

```http
https://api-us.securitycenter.microsoft.com/api/DeviceAuthenticatedScanAgents
```

### Response example

Here's an example of the response.

```json
{
    "@odata.context": "https://api-us.securitycenter.microsoft.com/api/$metadata#DeviceAuthenticatedScanAgents",
    "value": [
        {
            "id": "47df41a0c-asad-4fd6d3-bbea-a93dbc0bfcaa_4edd75b2407a5b64d704b4e53d74f15",
            "machineId": "4ejh675b240118fbehiuiy5b64d704b4e53d15",
            "lastSeen": "2022-05-08T12:18:41.538203Z",
            "computerDnsName": "TEST_DOMAIN",
            "AssignedApplicationId": "9E0FA0EB-0A51-4357-9C87-C21BFBE07571",
            "ScannerSoftwareVersion": "7.1.1",
            "LastCommandExecutionTimestamp": "2022-05-08T12:18:41.538203Z",
            "mdeClientVersion": "10.8295.22621.1195"
        },
        {
            "id": "47d41a0c-1dfd-46d3-bbea-a93dbc0bfcaa_eb663a27ae9d032f61bc268oiu4c4b90f77",
            "machineId": "eb663a27ae9d032sdf9dfd79eedf14c4b90f77",
            "lastSeen": "2022-12-19T20:29:04.8242449Z",
            "computerDnsName": "TEST_DOMAIN2",
            "AssignedApplicationId": "9E0FA0EB-0A51-4357-9C87-C21BFBE07571",
            "ScannerSoftwareVersion": "7.1.1",
            "LastCommandExecutionTimestamp": "2022-12-19T20:29:04.8242449Z",
            "mdeClientVersion": "10.8295.22621.1010"
        },
    ]
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
