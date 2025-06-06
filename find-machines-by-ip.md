---
title: Find devices by internal IP API
description: Find devices seen with the requested internal IP in the time range of 15 minutes prior and after a given timestamp
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

# Find devices by internal IP API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]


**Applies to:** 
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!Include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!Include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Find [Machines](machine.md) seen with the requested internal IP in the time range of 15 minutes prior and after a given timestamp.

## Limitations

1. The given timestamp must be in the past 30 days.
2. Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

Permission type|Permission|Permission display name
:---|:---|:---
Application|Machine.Read.All|'Read all machine profiles'
Application|Machine.ReadWrite.All|'Read and write all machine information'
Delegated (work or school account)|Machine.Read|'Read machine information'
Delegated (work or school account)|Machine.ReadWrite|'Read and write machine information'

> [!NOTE]
> When obtaining a token using user credentials:
>
> - Response will include only devices that the user have access to based on device group settings (For more information, see [Create and manage device groups](../machine-groups.md))
> - The user needs to have at least the following role permission: 'View Data' (For more information, see [Create and manage roles](../user-roles.md))
> - Response will include only devices that the user have access to based on device group settings (For more information, see [Create and manage device groups](../machine-groups.md))
>
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## HTTP request

```http
GET /api/machines/findbyip(ip='{IP}',timestamp={TimeStamp})
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization|String|Bearer {token}. **Required**.

## Request body

Empty

## Response

If successful - 200 OK with list of the machines in the response body.
If the timestamp isn't in the past 30 days - 400 Bad Request.

## Example

### Request

Here's an example of the request.

```http
GET https://api.securitycenter.microsoft.com/api/machines/findbyip(ip='10.248.240.38',timestamp=2019-09-22T08:44:05Z)
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
