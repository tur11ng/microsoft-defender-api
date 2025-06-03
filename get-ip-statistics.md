---
title: Get IP statistics API
description: Get the latest stats for your IP using Microsoft Defender for Endpoint.
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
ms.date: 04/17/2024
---

# Get IP statistics API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description
Retrieves the statistics for the given IP.

## Limitations
1. Rate limitations for this API are 100 calls per minute and 1500 calls per hour.
2. Maximum Value for Lookbackhours is 720 Hours(30days).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

Permission type|Permission|Permission display name
:---|:---|:---
Application|Ip.Read.All|'Read IP address profiles'
Delegated (work or school account)|Ip.Read.All|'Read IP address profiles'

> [!NOTE]
> When obtaining a token using user credentials:
> - The user needs to have at least the following role permission: 'View Data' (For more information, see [Create and manage roles](../user-roles.md))

## HTTP request

```http
GET /api/ips/{ip}/stats
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization|String|Bearer {token}. **Required**.

## Request URI parameters

Name|Type|Description
:---|:---|:---
lookBackHours|Int32|Defines the hours we search back to get the statistics. Defaults to 30 days. **Optional**.

## Request body

Empty

## Response

If successful and ip exists - 200 OK with statistical data in the body. IP is valid but doesn't exist - organizationPrevalence 0, IP is invalid - HTTP 400.

## Example

### Request example

Here's an example of the request.

```http
GET https://api.security.microsoft.com/api/ips/10.209.67.177/stats?lookBackHours=48
```

### Response example

Here's an example of the response.

```json
{
    "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgIPStats",
    "ipAddress": "10.209.67.177",
    "organizationPrevalence": 63515,
    "orgFirstSeen": "2017-07-30T13:36:06Z",
    "orgLastSeen": "2017-08-29T13:32:59Z"
}
```

|Name|Description|
|---|---|
|Organization prevalence|the distinct count of devices that opened network connection to this IP.|
|Org first seen|the first connection for this IP in the organization.|
|Org last seen|the last connection for this IP in the organization.|

> [!NOTE]
> This statistic information is based on data from the past 30 days.
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
