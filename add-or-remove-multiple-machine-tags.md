---
title: Add or remove a tag for multiple machines
description: Learn how to use the Add or Remove machine tags API to add or remove a tag for multiple devices in Microsoft Defender for Endpoint.
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
ms.date: 03/21/2025
---

# Add or remove a tag for multiple machines

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Adds or removes a tag for the specified set of machines.

## Limitations

1. You can post on machines last seen according to your configured retention period.
2. Rate limitations for this API are 100 calls per minute and 1,500 calls per hour.
3. We can add or remove a tag for up to 500 machines per API call.


## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Defender for Endpoint APIs](apis-intro.md).

Permission type|Permission|Permission display name
:---|:---|:---
Application|Machine.ReadWrite.All|'Read and write all machine information'
Delegated (work or school account)|Machine.ReadWrite|'Read and write machine information'

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have at least the following role permission: 'Manage security setting'. For more information, see [Create and manage roles](../user-roles.md).
> - The user needs to have access to the machine, based on machine group settings (See [Create and manage machine groups](../machine-groups.md) for more information).

## HTTP request

```http
POST https://api.securitycenter.microsoft.com/api/machines/AddOrRemoveTagForMultipleMachines
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization|String|Bearer {token}. **Required**.
Content-Type|string|application/json. **Required**.

## Request body

In the request body, supply a JSON object with the following parameters:

Parameter|Type|Description
:---|:---|:---
Value|String|The tag name. **Required**.
Action|Enum|Add or Remove. Allowed values are: 'Add' or 'Remove'. **Required**.
MachineIds|List (String)|List of machine IDs to update. Required.|

## Response

If successful, this method returns 200 - Ok response code and the updated machines in the response body.

## Example Request

Here's an example of a request that adds a tag to multiple machines.

```http
POST https://api.securitycenter.microsoft.com/api/machines/AddOrRemoveTagForMultipleMachines
```

```json
{
  "Value" : "Tag",
  "Action": "Add",
  "MachineIds": ["34e83ca3feea4dae2353006ba389262c033a025e",
  "2a398439b4975924e87a65943972bc702469b329",
  "a610c00c65fdf79960cc0077d9d8c569d23f09a5"]
}
```

To remove machine tags, set the Action to 'Remove' instead of 'Add' in the request body.
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
