---
title: Investigation resource type
description: Microsoft Defender for Endpoint Investigation entity.
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

# Investigation resource type

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!Include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!Include[Improve request performance](../../includes/improve-request-performance.md)]

Represent an Automated Investigation entity in Defender for Endpoint.

For more information, see [Overview of automated investigations](../automated-investigations.md).

## Methods

Method|Return Type|Description
:---|:---|:---
[List Investigations](get-investigation-collection.md)|Investigation collection|Get collection of Investigation
[Get single Investigation](get-investigation-object.md)|Investigation entity|Gets single Investigation entity.
[Start Investigation](initiate-autoir-investigation.md)|Investigation entity|Starts Investigation on a device.

## Properties

Property|Type|Description
:---|:---|:---
ID|String|Identity of the investigation entity. 
startTime|DateTime Nullable|The date and time when the investigation was created.
endTime|DateTime Nullable|The date and time when the investigation was completed.
cancelledBy|String|The ID of the user/application that canceled that investigation.
State|Enum|The current state of the investigation. Possible values are: 'Unknown', 'Terminated', 'SuccessfullyRemediated', 'Benign', 'Failed', 'PartiallyRemediated', 'Running', 'PendingApproval', 'PendingResource', 'PartiallyInvestigated', 'TerminatedByUser', 'TerminatedBySystem', 'Queued', 'InnerFailure', 'PreexistingAlert', 'UnsupportedOs', 'UnsupportedAlertType', 'SuppressedAlert'.
statusDetails|String|Additional information about the state of the investigation.
machineId|String|The ID of the device on which the investigation is executed.
computerDnsName|String|The name of the device on which the investigation is executed.
triggeringAlertId|String|The ID of the alert that triggered the investigation.

## Json representation

```json
{
    "id": "63004",
    "startTime": "2020-01-06T13:05:15Z",
    "endTime": null,
    "state": "Running",
    "cancelledBy": null,
    "statusDetails": null,
    "machineId": "e828a0624ed33f919db541065190d2f75e50a071",
    "computerDnsName": "desktop-test123",
    "triggeringAlertId": "da637139127150012465_1011995739"
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
