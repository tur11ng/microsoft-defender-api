---
title: machineAction resource type
description: Learn about the methods and properties of the MachineAction resource type in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
ms.topic: conceptual
ms.custom: api
ms.subservice: reference
search.appverid: met150
ms.date: 03/01/2025
---

# MachineAction resource type

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business) (for supported capabilities only)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)


[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]


- For more information, see [Response Actions](../respond-machine-alerts.md).
- If you're using Defender for Business, see [Review remediation actions](/defender-business/mdb-review-remediation-actions) for available actions.

|Method|Return Type|Description|
|---|---|---|
|[List MachineActions](get-machineactions-collection.md)|[Machine Action](machineaction.md)|List [Machine Action](machineaction.md) entities.|
|[Get MachineAction](get-machineaction-object.md)|[Machine Action](machineaction.md)|Get a single [Machine Action](machineaction.md) entity.|
|[Collect investigation package](collect-investigation-package.md)|[Machine Action](machineaction.md)|Collect investigation package from a [machine](machine.md).|
|[Get investigation package SAS URI](get-package-sas-uri.md)|[Machine Action](machineaction.md)|Get URI for downloading the investigation package.|
|[Isolate machine](isolate-machine.md)|[Machine Action](machineaction.md)|Isolate [machine](machine.md) from network.|
|[Release machine from isolation](unisolate-machine.md)|[Machine Action](machineaction.md)|Release [machine](machine.md) from Isolation.|
|[Restrict app execution](restrict-code-execution.md)|[Machine Action](machineaction.md)|Restrict application execution.|
|[Remove app restriction](unrestrict-code-execution.md)|[Machine Action](machineaction.md)|Remove application execution restriction.|
|[Run antivirus scan](run-av-scan.md)|[Machine Action](machineaction.md)|Run an AV scan using Windows Defender (when applicable).|
|[Offboard machine](offboard-machine-api.md)|[Machine Action](machineaction.md)|Offboard [machine](machine.md) from Microsoft Defender for Endpoint.|
|[Stop and quarantine file](stop-and-quarantine-file.md)|[Machine Action](machineaction.md)|Stop execution of a file on a machine and delete it.|
|[Run live response](run-live-response.md)|[Machine Action](machineaction.md)|Runs a sequence of live response commands on a device|
|[Get live response result](get-live-response-result.md)|URL entity|Retrieves specific live response command result download link by its index.|
|[Cancel machine action](cancel-machine-action.md)|[Machine Action](machineaction.md)|Cancel an active machine action.|

<br>

## Properties

|Property|Type|Description|
|---|---|---|
|ID|Guid|Identity of the [Machine Action](machineaction.md) entity.|
|type|Enum|Type of the action. Possible values are: `RunAntiVirusScan`, `Offboard`, `LiveResponse`, `CollectInvestigationPackage`, `Isolate`, `Unisolate`, `StopAndQuarantineFile`, `RestrictCodeExecution`, and `UnrestrictCodeExecution`.|
|scope|string|Scope of the action. `Full` or `Selective` for Isolation, `Quick` or `Full` for antivirus scan.|
|requestor|String|Identity of the person that executed the action.|
|externalID|String|Id the customer can submit in the request for custom correlation.|
|requestSource|string|The name of the user/application that submitted the action.|
|commands|array|Commands to run. Allowed values are PutFile, RunScript, GetFile.|
|cancellationRequestor|String|Identity of the person that canceled the action.|
|requestorComment|String|Comment that was written when issuing the action.|
|cancellationComment|String|Comment that was written when canceling the action.|
|status|Enum|Current status of the command. Possible values are: `Pending`, `InProgress`, `Succeeded`, `Failed`, `TimeOut`, and `Cancelled`.|
|machineId|String|ID of the [machine](machine.md) on which the action was executed.|
|computerDnsName|String|Name of the [machine](machine.md) on which the action was executed.|
|creationDateTimeUtc|DateTimeOffset|The date and time when the action was created.|
|cancellationDateTimeUtc|DateTimeOffset|The date and time when the action was canceled.|
|lastUpdateDateTimeUtc|DateTimeOffset|The last date and time when the action status was updated.|
|title|String|Machine action title.|
|relatedFileInfo|Class|Contains two Properties. string `fileIdentifier`, Enum `fileIdentifierType` with the possible values: `Sha1`, `Sha256`, and `Md5`.|

## Json representation

```json
{
        "id": "5382f7ea-7557-4ab7-9782-d50480024a4e",
        "type": "Isolate",
        "scope": "Selective",
        "requestor": "Analyst@TestPrd.onmicrosoft.com",
        "requestorComment": "test for docs",
        "status": "Succeeded",
        "machineId": "7b1f4967d9728e5aa3c06a9e617a22a4a5a17378",
        "computerDnsName": "desktop-test",
        "creationDateTimeUtc": "2019-01-02T14:39:38.2262283Z",
        "lastUpdateDateTimeUtc": "2019-01-02T14:40:44.6596267Z",
        "relatedFileInfo": null
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
