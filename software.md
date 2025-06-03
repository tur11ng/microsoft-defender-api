---
title: Software methods and properties
description: Retrieves top recent alerts.
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

# Software resource type

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

[!include[Prerelease information](../../includes/prerelease.md)]

## Methods

|Method|Return Type|Description|
|---|---|---|
|[List software](get-software.md)|Software collection|List the organizational software inventory|
|[Get software by ID](get-software-by-id.md)|Software|Get a specific software by its software ID|
|[List software version distribution](get-software-ver-distribution.md)|Distribution collection|List software version distribution by software ID|
|[List machines by software](get-machines-by-software.md)|MachineRef collection|Retrieve a list of devices that are associated with the software ID|
|[List vulnerabilities by software](get-vuln-by-software.md)|[Vulnerability](vulnerability.md) collection|Retrieve a list of vulnerabilities associated with the software ID|
|[Get missing KBs](get-missing-kbs-software.md)|KB collection|Get a list of missing KBs associated with the software ID|


## Properties

|Property|Type|Description|
|---|---|---|
|id|String|Software ID|
|Name|String|Software name|
|Vendor|String|Software publisher name|
|Weaknesses|Long|Number of discovered vulnerabilities|
|publicExploit|Boolean|Public exploit exists for some of the vulnerabilities|
|activeAlert|Boolean|Active alert is associated with this software|
|exposedMachines|Long|Number of exposed devices|
|impactScore|Double|Exposure score impact of this software|

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
