---
title: Machine resource type
description: Learn about the methods and properties of the Machine resource type in Microsoft Defender for Endpoint.
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

# Machine resource type

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

[!include[Prerelease information](../../includes/prerelease.md)]

## Methods

|Method|Return Type|Description|
|---|---|---|
|[List machines](get-machines.md)|[machine](machine.md) collection|List set of [machine](machine.md) entities in the org.|
|[Get machine](get-machine-by-id.md)|[machine](machine.md)|Get a [machine](machine.md) by its identity.|
|[Get logged on users](get-machine-log-on-users.md)|[user](user.md) collection|Get the set of [User](user.md) that logged on to the [machine](machine.md).|
|[Get related alerts](get-machine-related-alerts.md)|[alert](alerts.md) collection|Get the set of [alert](alerts.md) entities that were raised on the [machine](machine.md).|
|[Get installed software](get-installed-software.md)|[software](software.md) collection|Retrieves a collection of installed software related to a given machine ID.|
|[Get discovered vulnerabilities](get-discovered-vulnerabilities.md)|[vulnerability](vulnerability.md) collection|Retrieves a collection of discovered vulnerabilities related to a given machine ID.|
|[Get security recommendations](get-security-recommendations.md)|[recommendation](recommendation.md) collection|Retrieves a collection of security recommendations related to a given machine ID.|
|[Add or Remove machine tags](add-or-remove-machine-tags.md)|[machine](machine.md)|Add or Remove tag to a specific machine.|
|[Find machines by IP](find-machines-by-ip.md)|[machine](machine.md) collection|Find machines seen with IP.|
|[Find machines by tag](find-machines-by-tag.md)|[machine](machine.md) collection|Find machines by [Tag](../machine-tags.md).|
|[Get missing KBs](get-missing-kbs-machine.md)|KB collection|Get a list of missing KBs associated with the machine ID|
|[Set device value](set-device-value.md)|[machine](machine.md) collection|Set the [value of a device](/defender-vulnerability-management/tvm-assign-device-value).|
|[Update machine](update-machine-method.md)|[machine](machine.md) collection|Get the update status of a machine.|

## Properties

|Property|Type|Description|
|---|---|---|
|id|String|[machine](machine.md) identity.|
|computerDnsName|String|[machine](machine.md) fully qualified name.|
|firstSeen|DateTimeOffset|First date and time where the [machine](machine.md) was observed by Microsoft Defender for Endpoint.|
|lastSeen|DateTimeOffset|Time and date of the last received full device report. A device typically sends a full report every 24 hours. <br> NOTE: This property doesn't correspond to the last seen value in the UI. It pertains to the last device update.|
|osPlatform|String|Operating system platform.|
|onboardingstatus|String|Status of machine onboarding. Possible values are: `onboarded`, `CanBeOnboarded`, `Unsupported`, and `InsufficientInfo`.|
|osProcessor|String|Operating system processor. Use osArchitecture property instead.|
|version|String|Operating system Version.|
|osBuild|Nullable long|Operating system build number.|
|lastIpAddress|String|Last IP on local NIC on the [machine](machine.md).|
|lastExternalIpAddress|String|Last IP through which the [machine](machine.md) accessed the internet.|
|healthStatus|Enum|[machine](machine.md) health status. Possible values are: `Active`, `Inactive`, `ImpairedCommunication`, `NoSensorData`, `NoSensorDataImpairedCommunication`, and `Unknown`.|
|rbacGroupName|String|Machine group Name.|
|rbacGroupId|String|Machine group ID.|
|riskScore|Nullable Enum|Risk score as evaluated by Microsoft Defender for Endpoint. Possible values are: `None`, `Informational`, `Low`, `Medium`, and `High`.|
|aadDeviceId|Nullable representation Guid|Microsoft Entra Device ID (when [machine](machine.md) is Microsoft Entra joined).|
|machineTags|String collection|Set of [machine](machine.md) tags.|
|exposureLevel|Nullable Enum|Exposure level as evaluated by Microsoft Defender for Endpoint. Possible values are: `None`, `Low`, `Medium`, and `High`.|
|deviceValue|Nullable Enum|The [value of the device](/defender-vulnerability-management/tvm-assign-device-value). Possible values are: `Normal`, `Low`, and `High`.|
|ipAddresses|IpAddress collection|Set of ***IpAddress*** objects. See [Get machines API](get-machines.md).|
|osArchitecture|String|Operating system architecture. Possible values are: `32-bit`, `64-bit`. Use this property instead of osProcessor.|

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
