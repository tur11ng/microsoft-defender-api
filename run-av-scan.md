---
title: Run antivirus scan API
description: Use this API to create calls related to running an antivirus scan on a device.
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

# Run antivirus scan API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:** 
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](/defender-business)


> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Initiate Microsoft Defender Antivirus scan on a device.

## Limitations

1. Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

[!include[Device actions note](../../includes/machineactionsnote.md)]

> [!IMPORTANT]
>
> - This action is available for devices on Windows 10, version  1709 or later, and on Windows 11.
> - A Microsoft Defender Antivirus scan can run alongside other antivirus solutions, whether Microsoft Defender Antivirus is the active antivirus solution or not. Microsoft Defender Antivirus can be in Passive mode. For more information, see [Microsoft Defender Antivirus compatibility](../microsoft-defender-antivirus-compatibility.md).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

Permission type|Permission|Permission display name
:---|:---|:---
Application|Machine.Scan|'Scan machine'
Delegated (work or school account)|Machine.Scan|'Scan machine'

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have at least the following role permission: 'Active remediation actions' (See [Create and manage roles](../user-roles.md) for more information)
> - The user needs to have access to the device, based on device group settings (See [Create and manage device groups](../machine-groups.md) for more information)
> 
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.  

## HTTP request

```http
POST https://api.security.microsoft.com/api/machines/{id}/runAntiVirusScan
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization|String|Bearer {token}. **Required**.
Content-Type|string|application/json

## Request body

In the request body, supply a JSON object with the following parameters:

Parameter|Type|Description
:---|:---|:---
Comment|String|Comment to associate with the action. **Required**.
ScanType|String|Defines the type of the Scan. **Required**.

**ScanType** controls the type of scan to perform and can be one of the following:

- **Quick**: Perform quick scan on the device
- **Full**: Perform full scan on the device

## Response

If successful, this method returns 201, Created response code and _MachineAction_ object in the response body.

If you send  multiple API calls to run an antivirus scan for the same device, it returns "pending machine action" or HTTP 400 with the message "Action is already in progress".

## Example

### Request

Here is an example of the request.

```http
POST https://api.security.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/runAntiVirusScan 
```

```json
{
  "Comment": "Check machine for viruses due to alert 3212",
  "ScanType": "Full"
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
