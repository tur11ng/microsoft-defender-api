---
title: Get scan history by session
description: Learn how to use the get scan history by session api.
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
ms.date: 03/01/2025
---

# Get scan history by session

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

> Want to experience Microsoft Defender Vulnerability Management? Learn more about how you can sign up to the [Microsoft Defender Vulnerability Management public preview trial](/defender-vulnerability-management/get-defender-vulnerability-management).

[!Include[Prerelease information](../../includes/prerelease.md)]

[!Include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!Include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Retrieves a list of the scan history by session.

## Limitations

1. Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md).

Permission type|Permission|Permission display name
:---|:---|:---
Application|Machine.Read.All| Read all scan information.
Delegated (work or school account)|Machine.Read.All|Read all scan information.

> [!NOTE]
> When obtaining a token using user credentials:
>
> - To view data the user needs to have at least the following role permission: `ViewData` or `TvmViewData`. For more information, see [Create and manage roles](../user-roles.md).

## HTTP request

```http
POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization|string|Bearer {token}. **Required**.
Content-Type|string|application/json. **Required**.

## Request body

In the request body, supply a JSON object with the following parameters:

Parameter|Type|Description
:---|:---|:---
SessionIds |String|The session Id. **Required**.

## Response

If successful, this method returns 200 - OK response code with a list of the scan history for a session.

## Example request

Here's an example of the request.

```http
POST https://api.securitycenter.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId
```

```json
{
    "SessionIds": ["01decc497f4b4ec49a5fc4e12597f8c8"]
}
```

## Response example

```json
{
 "@odata.context": "https://api.securitycenter.microsoft.com/api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId",
    "value": [
    {
     "orgId": "asdf781a0c-792d-46d3-bbea-a93dbc0bfcaa",
     "ScanDefinitionIds": "4ad8d463-6b3a-4894-b42a-a2de9ea0a8ae",
     "SessionIds": "01decc497f4b4ec49a5fc4e12597f8c8",
     "NumberOfSuccessfullyScannedTargets": 3,
     "NumberOfTargets": 3,
     "ScanStatus": "Success",
     "LastScanned": "2022-12-19T15:14:24.5561791Z",
     "ListScannedTargets": {
         "Ip": "127.0.0.1",
         "Hostname": "DESKTOP-Test",
         "ScannedDeviceDescription": "Network device",
         "ErrorMessage": "",
         "ScanStatus": "Success",
         "ScanDuration": "00:08:30",
        },
        {
         "Ip": "127.0.0.2",
         "Hostname": "DESKTOP-Test2",
         "ScannedDeviceDescription": "Network device 2",
         "ErrorMessage": "",
         "ScanStatus": "Success",
         "ScanDuration": "00:08:00",
        },
{
         "Ip": "127.0.0.3",
         "Hostname": "DESKTOP-Test3",
         "ScannedDeviceDescription": "Network device 3",
         "ErrorMessage": "",
         "ScanStatus": "Success",
         "ScanDuration": "00:08:50",
        },
    }
  ]
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
