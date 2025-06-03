---
title: Supported Microsoft Defender for Endpoint APIs
ms.reviewer: 
description: Learn about the specific supported Microsoft Defender for Endpoint entities where you can create API calls to.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
ms.date: 03/21/2025
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
---

# Supported Microsoft Defender for Endpoint APIs

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:** 

- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](/defender-business)

> [!IMPORTANT]
> Advanced hunting capabilities are not included in Defender for Business. 


> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

## Endpoint URI and versioning

### Endpoint URI

> The service base URI is: [https://api.security.microsoft.com](https://api.security.microsoft.com)
> 
> The queries based OData have the '/api' prefix. For example, to get Alerts you can send GET request to [https://api.security.microsoft.com/api/alerts](https://api.security.microsoft.com/api/alerts)

### Versioning

> The API supports versioning.
> > The current version is **V1.0**.
> > To use a specific version, use this format: `https://api.security.microsoft.com/api/{Version}`. For example: `https://api.security.microsoft.com/api/v1.0/alerts`
> 
> If you don't specify any version (e.g. `https://api.security.microsoft.com/api/alerts`) you will get to the latest version.

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

Learn more about the individual supported entities where you can run API calls to and details such as HTTP request values, request headers and expected responses.

## In this section

Topic | Description
:---|:---
[**Advanced Hunting** methods](run-advanced-query-api.md) | Run queries from API.
[**Alert** methods and properties](alerts.md) | Run API calls such as \- get alerts, create alert, update alert and more.
[Export **Assessment** per-device methods and properties](get-assessment-methods-properties.md) | Run API calls to gather vulnerability assessments on a per-device basis, such as: \- export secure configuration assessment, export software inventory assessment,  export software vulnerabilities assessment, and delta export software vulnerabilities assessment.
[**Automated investigation** methods and properties](investigation.md) | Run API calls such as \- get collection of Investigation.
[Export device health methods and properties](device-health-api-methods-properties.md) | Run API Calls such as \- GET /api/public/avdeviceshealth.
[**Domain**-related alerts](get-domain-related-alerts.md) | Run API calls such as \- get domain-related devices, domain statistics and more.
[**File** methods and properties](files.md) | Run API calls such as \- get file information, file related alerts, file related devices, and file statistics.
[**Indicators** methods and properties](ti-indicator.md) | Run API call such as \- get Indicators, create Indicator, and delete Indicators.
[**IP**-related alerts](get-ip-related-alerts.md) | Run API calls such as \- get IP-related alerts and get IP statistics.
[**Machine** methods and properties](machine.md) | Run API calls such as \- get devices, get devices by ID, information about logged on users, edit tags and more.
[**Machine Action** methods and properties](machineaction.md) | Run API call such as \- Isolation, Run anti-virus scan and more.
[**Recommendation** methods and properties](recommendation.md) | Run API calls such as \- get recommendation by ID.
[**Remediation activity** methods and properties](get-remediation-methods-properties.md) | Run API call such as \- get all remediation tasks, get exposed devices remediation task and get one remediation task by id.
[**Score** methods and properties](score.md) | Run API calls such as \- get exposure score or get device secure score.
[**Software** methods and properties](software.md) | Run API calls such as \- list vulnerabilities by software.
[**User** methods and properties](user.md) | Run API calls such as \- get user-related alerts and user-related devices.
[**Vulnerability** methods and properties](vulnerability.md) | Run API calls such as \- list devices by vulnerability.

## See also

- [Microsoft Defender for Endpoint APIs](apis-intro.md)

- [Microsoft Defender for Endpoint API release notes](api-release-notes.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
