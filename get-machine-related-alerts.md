---
title: Get machine related alerts API
description: Learn how to use the Get machine related alerts API. This API allows you to retrieve all alerts that are related to a specific device in Microsoft Defender for Endpoint.
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

# Get machine related alerts  API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:** 
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Retrieves all [Alerts](alerts.md) related to a specific device.

## Limitations

1. You can query on devices last updated according to your configured retention period.
2. Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

Permission type|Permission|Permission display name
:---|:---|:---
Application|Alert.Read.All|'Read all alerts'
Application|Alert.ReadWrite.All|'Read and write all alerts'
Delegated (work or school account) | Alert.Read | 'Read alerts'
Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts'

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have at least the following role permission: 'View Data'. For more information about permissions, see [Create and manage roles](../user-roles.md).
> - The user needs to have access to the device, based on device group settings. For more information about device group settings, see [Create and manage device groups](../machine-groups.md).
>
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.
## HTTP request

```http
GET /api/machines/{id}/alerts
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization | String | Bearer {token}. **Required**.

## Request body

Empty

## Response

If successful and device exists: 200 OK with list of [alert](alerts.md) entities in the body. If device was not found: 404 Not Found.
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
