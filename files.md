---
title: File resource type
description: Retrieve recent Microsoft Defender for Endpoint alerts related to files.
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

# File resource type

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]


**Applies to:** 
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

Represent a file entity in Defender for Endpoint.

## Methods

|Method|Return Type |Description|
|:---|:---|:---|
|[Get file](get-file-information.md) | [file](files.md) | Get a single file |
|[List file related alerts](get-file-related-alerts.md) | [alert](alerts.md) collection | Get the [alert](alerts.md) entities that are associated with the file.|
|[List file related machines](get-file-related-machines.md) | [machine](machine.md) collection | Get the [machine](machine.md) entities associated with the alert.|
|[file statistics](get-file-statistics.md) | Statistics summary | Retrieves the prevalence for the given file.|


## Properties

|Property | Type | Description |
|:---|:---|:---|
|sha1 | String | Sha1 hash of the file content |
|sha256 | String | Sha256 hash of the file content |
|globalPrevalence | Nullable long | File prevalence across organization |
|globalFirstObserved | DateTimeOffset | First time the file was observed |
|globalLastObserved | DateTimeOffset | Last time the file was observed |
|size | Nullable long | Size of the file |
|fileType | String | Type of the file |
|isPeFile | Boolean | true if the file is portable executable (for example `DLL`, `EXE`, etc.) |
|filePublisher | String | File publisher |
|fileProductName | String | Product name |
|signer | String | File signer |
|issuer | String | File issuer |
|signerHash | String | Hash of the signing certificate |
|isValidCertificate | Boolean | Was signing certificate successfully verified by Microsoft Defender for Endpoint agent |
|determinationType | String | The determination type of the file |
|determinationValue | String | Determination value |

## Json representation

```json
{
    "sha1": "4388963aaa83afe2042a46a3c017ad50bdcdafb3",
    "sha256": "413c58c8267d2c8648d8f6384bacc2ae9c929b2b96578b6860b5087cd1bd6462",
    "globalPrevalence": 180022,
    "globalFirstObserved": "2017-09-19T03:51:27.6785431Z",
    "globalLastObserved": "2020-01-06T03:59:21.3229314Z",
    "size": 22139496,
    "fileType": "APP",
    "isPeFile": true,
    "filePublisher": "CHENGDU YIWO Tech Development Co., Ltd.",
    "fileProductName": "EaseUS MobiSaver for Android",
    "signer": "CHENGDU YIWO Tech Development Co., Ltd.",
    "issuer": "VeriSign Class 3 Code Signing 2010 CA",
    "signerHash": "6c3245d4a9bc0244d99dff27af259cbbae2e2d16",
    "isValidCertificate": false,
    "determinationType": "Pua",
    "determinationValue": "PUA:Win32/FusionCore"
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
