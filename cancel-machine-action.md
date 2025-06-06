---
title: Cancel machine action API
description: Learn how to cancel an already launched machine action
search.appverid: met150
ms.service: defender-endpoint
ms.subservice: reference
f1.keywords:
- NOCSH
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
ms.custom: api
ms.date: 03/21/2025
---

# Cancel machine action API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint](/defender-xdr/microsoft-365-security-center-mde)
- [Microsoft Defender for Endpoint Plan 1](../defender-endpoint-plan-1.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)

[!include[Prerelease information](../../includes/prerelease.md)]

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Cancel an already launched machine action that isn't yet in final state (completed, canceled, failed).

## Limitations

1. Rate limitations for this API are 100 calls per minute and 1500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more,
including how to choose permissions, see [Get started](apis-intro.md).

|Permission type|Permission|Permission display name|
|---|---|---|
|Application|Machine.CollectForensics <br> Machine.Isolate <br> Machine.RestrictExecution <br> Machine.Scan <br> Machine.Offboard <br> Machine.StopAndQuarantine <br> Machine.LiveResponse|Collect forensics <br>Isolate machine<br>Restrict code execution<br>  Scan machine<br>  Offboard machine<br> Stop And Quarantine<br> Run live response on a specific machine|
|Delegated (work or school account)|Machine.CollectForensics<br> Machine.Isolate  <br>Machine.RestrictExecution<br> Machine.Scan<br> Machine.Offboard<br> Machine.StopAndQuarantineMachine.LiveResponse|Collect forensics<br> Isolate machine<br>  Restrict code execution<br> Scan machine<br>Offboard machine<br> Stop And Quarantine<br> Run live response on a specific machine|

## HTTP request

```http
POST https://api.securitycenter.microsoft.com/api/machineactions/<machineactionid>/cancel
```

## Request headers

|Name|Type|Description|
|---|---|---|
|Authorization|String|Bearer {token}. Required.|
|Content-Type|string|application/json. Required.|

## Request body

|Parameter|Type|Description|
|---|---|---|
|Comment|String|Comment to associate with the cancellation action.|

## Response

If successful, this method returns 200, OK response code with a Machine Action entity. If machine action entity with the specified id wasn't found - 404 Not Found.

## Example

### Request

Here's an example of the request.

```HTTP
POST
https://api.securitycenter.microsoft.com/api/machineactions/988cc94e-7a8f-4b28-ab65-54970c5d5018/cancel
```

```JSON
{
    "Comment": "Machine action was canceled by automation"
}
```

## Related article

- [Get machine action API](get-machineaction-object.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
