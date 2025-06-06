---
title: Microsoft Defender for Endpoint API release notes
description: Release notes for updates made to the Microsoft Defender for Endpoint set of APIs.
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

# Microsoft Defender for Endpoint API release notes

**Applies to:** 
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

The following information lists the updates made to the Microsoft Defender for Endpoint APIs and the dates they were made.

## Release notes - newest to oldest (dd.mm.yyyy)

### 08.08.2022

- Added new Export Device Health API method - GET /api/public/avdeviceshealth [Export device health methods and properties](device-health-api-methods-properties.md)

### 06.10.2021

- Added new Export assessment API method  - _Delta Export software vulnerabilities assessment (JSON response)_ [Export assessment methods and properties per device](get-assessment-methods-properties.md).

### 25.05.2021

- Added new API [Export assessment methods and properties per device](get-assessment-methods-properties.md).

### 03.05.2021

- Added new API: [Remediation activity methods and properties](get-remediation-methods-properties.md).

### 10.02.2021

- Added new API: [Batch update alerts](batch-update-alerts.md).

### 25.01.2021

- Updated rate limitations for [Advanced Hunting API](run-advanced-query-api.md) from 15 to 45 requests per minute.

### 21.01.2021

- Added new API: [Find devices by tag](../machine-tags.md).
- Added new API: [Import Indicators](import-ti-indicators.md).

### 03.01.2021

- Updated Alert evidence: added ***detectionStatus***, ***parentProcessFilePath*** and ***parentProcessFileName*** properties.
- Updated [Alert entity](alerts.md): added ***detectorId*** property.

### 15.12.2020

- Updated [Device](machine.md) entity: added ***IpInterfaces*** list. See [List devices](get-machines.md).

### 04.11.2020

- Added new API: [Set device value](set-device-value.md).
- Updated [Device](machine.md) entity: added ***deviceValue*** property.

### 01.09.2020

- Added option to expand the Alert entity with its related Evidence. See [List Alerts](get-alerts.md).
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
