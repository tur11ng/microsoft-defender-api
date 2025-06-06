---
title: Batch Update alert entities API
description: Learn how to update Microsoft Defender for Endpoint alerts in a batch by using this API. You can update the status, determination, classification, and assignedTo properties.
ms.service: defender-endpoint
ms.subservice: reference
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
search.appverid: met150
ms.date: 03/21/2025
---

# Batch update alerts

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]


**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Updates properties of a batch of existing [Alerts](alerts.md).

Submission of **comment** is available with or without updating properties.

Updatable properties are: `status`, `determination`, `classification` and `assignedTo`.

## Limitations

1. You can update alerts that are available in the API. For more information, see [List Alerts](get-alerts.md).
2. Rate limitations for this API are 10 calls per minute and 500 calls per hour.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

Permission type | Permission | Permission display name
:---|:---|:---
Application | Alert.ReadWrite.All | 'Read and write all alerts'
Delegated (work or school account) | Alert.ReadWrite | 'Read and write alerts'

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have at least the following role permission: 'Alerts investigation'. For more information, see [Create and manage roles](../user-roles.md).
> - The user needs to have access to the device associated with the alert, based on device group settings. For more information, see [Create and manage device groups](../machine-groups.md).
>
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

## HTTP request

```http
POST /api/alerts/batchUpdate
```

## Request headers

Name|Type|Description
:---|:---|:---
Authorization | String | Bearer {token}. **Required**.
Content-Type | String | application/json. **Required**.

## Request body

In the request body, supply the IDs of the alerts to be updated and the values of the relevant fields that you wish to update for these alerts.

Existing properties that aren't included in the request body will maintain their previous values or be recalculated based on changes to other property values.

For best performance you shouldn't include existing values that haven't changed.

Property | Type | Description
:---|:---|:---
alertIds | List&lt;String&gt;| A list of the IDs of the alerts to be updated. **Required**
status | String | Specifies the updated status of the specified alerts. The property values are: 'New', 'InProgress' and 'Resolved'.
assignedTo | String | Owner of the specified alerts
classification | String | Specifies the specification of the specified alerts. The property values are: `TruePositive`, `Informational, expected activity`, and `FalsePositive`.
determination | String | Specifies the determination of the specified alerts. <p>Possible determination values for each classification are: <br><li> <b>True positive</b>: `Multistage attack` (MultiStagedAttack), `Malicious user activity` (MaliciousUserActivity), `Compromised account` (CompromisedUser) – consider changing the enum name in public api accordingly, `Malware` (Malware), `Phishing` (Phishing), `Unwanted software` (UnwantedSoftware), and `Other` (Other). <li> <b>Informational, expected activity:</b> `Security test` (SecurityTesting), `Line-of-business application` (LineOfBusinessApplication), `Confirmed activity` (ConfirmedUserActivity) - consider changing the enum name in public api accordingly, and `Other` (Other). <li>  <b>False positive:</b> `Not malicious` (Clean) - consider changing the enum name in public api accordingly, `Not enough data to validate` (InsufficientData), and `Other` (Other).
comment | String | Comment to be added to the specified alerts.

> [!NOTE]
> Around August 29, 2022, previously supported alert determination values ('Apt' and 'SecurityPersonnel') will be deprecated and no longer available via the API.

## Response

If successful, this method returns 200 OK, with an empty response body.

## Example

### Request

Here's an example of the request.

```http
POST https://api.securitycenter.microsoft.com/api/alerts/batchUpdate
```

```json
{
    "alertIds": ["da637399794050273582_760707377", "da637399989469816469_51697947354"],
    "status": "Resolved",
    "assignedTo": "secop2@contoso.com",
    "classification": "FalsePositive",
    "determination": "Malware",
    "comment": "Resolve my alert and assign to secop2"
}
```
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
