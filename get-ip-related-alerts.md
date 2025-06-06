---
title: Get IP related alerts API
description: Retrieve a collection of alerts related to a given IP address using Microsoft Defender for Endpoint.
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

# Get IP related alerts API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description
Retrieves a collection of alerts related to a given IP address.


## Limitations
1. Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.


## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Defender for Endpoint APIs](apis-intro.md).

|Permission type|Permission|Permission display name|
|:---|:---|:---|
|Application|Alert.Read.All|`Read all alerts`|
|Application|Alert.ReadWrite.All|`Read and write all alerts`|
|Delegated (work or school account) | Alert.Read | `Read alerts`|
|Delegated (work or school account) | Alert.ReadWrite | `Read and write alerts`|

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have at least the following role permission: `View Data`. For more information, see [Create and manage roles](../user-roles.md) for more information.
> - Response includes only alerts, associated with devices, that the user have access to, based on device group settings (See [Create and manage device groups](../machine-groups.md) for more information)
>
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## HTTP request

```http
GET /api/ips/{ip}/alerts
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization | String | Bearer {token}. **Required**.

## Request body

Empty

## Response

If successful and IP exists - 200 OK with list of [alert](alerts.md) entities in the body. If IP address is unknown but valid, it returns an empty set.
If the IP address is invalid, it returns HTTP 400.

## Example

### Request

Here's an example of the request.

```http
GET https://api.securitycenter.microsoft.com/api/ips/10.209.67.177/alerts
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
