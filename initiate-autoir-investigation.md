---
title: Start Investigation API
description: Use this API to start investigation on a device.
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

# Start Investigation API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Start automated investigation on a device.

See [Overview of automated investigations](../automated-investigations.md) for more information.

## Limitations

1. Rate limitations for this API are 50 calls per hour.

## Requirements for AIR

Your organization must have Defender for Endpoint (see [Minimum requirements for Microsoft Defender for Endpoint](../minimum-requirements.md).

Currently, AIR only supports the following OS versions:

- Windows 11
- Windows 10, version [1803](/windows/release-information/status-windows-10-1809-and-windows-server-2019) or later
- Windows 10, version 1803 (OS Build 17134.704 with [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464)) or later
- Windows 10, version 1709 (OS Build 16299.1085 with [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441)) or later
- Windows Server 2025
- Windows Server 2022
- Windows Server 2019

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

Permission type|Permission|Permission display name
:---|:---|:---
Application|Alert.ReadWrite.All|'Read and write all alerts'
Delegated (work or school account)|Alert.ReadWrite|'Read and write alerts'

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have at least the following role permission: 'Active remediation actions' (See [Create and manage roles](../user-roles.md) for more information)
> - The user needs to have access to the device, based on device group settings (See [Create and manage device groups](../machine-groups.md) for more information)
>
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2. 

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/startInvestigation
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
Comment|String|Comment to associate with the action. **Required**.

## Response

If successful, this method returns 201 - Created response code and [Investigation](investigation.md) in the response body.

## Example

### Request

Here is an example of the request.

```https
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/startInvestigation
```

```json
{
  "Comment": "Test investigation"
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
