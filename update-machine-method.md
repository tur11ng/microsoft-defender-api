---
title: Update machine entity API
description: Learn how to update machine tags by using this API. You can update the tags and devicevalue properties.
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

# Update machine 

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

Updates properties of existing [Machine](machine.md).

Updatable properties are: `machineTags` and `deviceValue`.

## Limitations

1. You can update machines that are available in the API. 
2. Update machine only appends tags to the tag collection. If tags exist, they must be included in the tags collection in the body.
3. Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

Permission type|Permission|Permission display name
:---|:---|:---
Application|Machine.ReadWrite.All|'Read and write machine information for all machines'
Delegated (work or school account)|Machine.ReadWrite|'Read and write machine information'

> [!NOTE]
> When obtaining a token using user credentials:
> - The user needs to have at least the following role permission: 'Alerts investigation'. For more information, see [Create and manage roles](../user-roles.md).
> - The user needs to have access to the device associated with the alert, based on device group settings. For more information, see [Create and manage device groups](../machine-groups.md).
>
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## HTTP request

```http
PATCH /api/machines/{machineId}
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization|String|Bearer {token}. **Required**.
Content-Type|String|application/json. **Required**.

## Request body

In the request body, supply the values for the relevant fields that should be updated.

Existing properties that aren't included in the request body will maintain their previous values or be recalculated based on changes to other property values.

For best performance, you shouldn't include existing values that haven't change.

Property|Type|Description
:---|:---|:---
machineTags|String collection|Set of [machine](machine.md) tags.
deviceValue|Nullable Enum|The [value of the device](/defender-vulnerability-management/tvm-assign-device-value). Possible values are: 'Normal', 'Low' and 'High'.

## Response

If successful, this method returns 200 OK, and the [machine](machine.md) entity in the response body with the updated properties.

If machine tags collection in body doesn't contain existing machine tags - replaces all tags with the tags provided in the request body.

If machine with the specified ID wasn't found - 404 Not Found.

## Example

### Request

Here's an example of the request.

```http
PATCH https://api.securitycenter.microsoft.com/api/machines/{machineId}
```

```json
{
    "deviceValue": "Normal",
    "machineTags": [
                     "Demo Device",
                     "Generic User Machine - Attack Source",
                     "Windows 10" "Windows11",
                     "Windows Insider - Fast"
    ]
}
```

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
