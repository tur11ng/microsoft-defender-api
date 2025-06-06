---
title: Get domain-related alerts API
description: Learn how to use the Get domain-related alerts API to retrieve alerts related to a given domain address in Microsoft Defender for Endpoint.
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

# Get domain-related alerts API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Retrieves a collection of [Alerts](alerts.md) related to a given domain address.

## Limitations

- You can query on alerts last updated according to your configured retention period.
- Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

Permission type|Permission|Permission display name
:---|:---|:---
Application|Alert.Read.All|'Read all alerts'
Application|Alert.ReadWrite.All|'Read and write all alerts'
Delegated (work or school account)|Alert.Read|'Read alerts'
Delegated (work or school account)|Alert.ReadWrite|'Read and write alerts'

When obtaining a token using user credentials, the user needs to have at least the following role permission: `View Data` (See [Create and manage roles](../user-roles.md)).

A response includes only alerts, associated with devices, that the user has access to, based on device group settings (See [Create and manage device groups](../machine-groups.md)).

Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## HTTP request

```http
GET /api/domains/{domain}/alerts
```

## Request headers

|Header|Value|
|---|---|
|Authorization|String|

## Request body

Empty

## Response

If successful and domain exists - 200 OK with list of [alert](alerts.md) entities. If domain doesn't exist - 200 OK with an empty set.

## Example

### Request

Here's an example of the request.

```http
GET https://api.securitycenter.microsoft.com/api/domains/client.wns.windows.com/alerts
```

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
