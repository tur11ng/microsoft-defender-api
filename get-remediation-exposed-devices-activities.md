---
title: List exposed devices of one remediation activity
description: Returns information about exposed devices for the specified remediation task.
ms.service: defender-endpoint
author: denisebmsft
ms.author: deniseb
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
ms.date: 04/25/2021
---

# List exposed devices of one remediation activity

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Prerelease information](../../includes/prerelease.md)]

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API Description

Returns information about exposed devices for the specified remediation task.

[Learn more about remediation activities](/defender-vulnerability-management/tvm-remediation).

## List exposed devices associated with a remediation task (id)

**URL:** GET: /api/remediationTasks/\{id\}/machineReferences

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs for details.](apis-intro.md)

Permission type|Permission|Permission display name
:---|:---|:---
Application|RemediationTasks.Read.All|\'Read Threat and Vulnerability Management vulnerability information\'
Delegated (work or school account)|RemediationTask.Read.Read|\'Read Threat and Vulnerability Management vulnerability information\'

## Properties details

Property (id)|Data type|Description|Example
:---|:---|:---|:---
id|String|Device ID|w2957837fwda8w9ae7f023dba081059dw8d94503
computerDnsName|String|Device name|PC-SRV2012R2Foo.UserNameVldNet.local
osPlatform|String|Device operating system|WindowsServer2012R2
rbacGroupName|String|Name of the device group this device is associated with|Servers

## Example

### Request example

```http
GET https://api.securitycenter.windows.com/api/remediationtasks/03942ef5-aecb-4c6e-b555-d6a97013844c/machinereferences
```

### Response example

```json
{
    "@odata.context": "https://api.securitycenter.windows.com/api/$metadata#MachineReferences",
    "value": [
        {
            "id": "3cb5df6bb3640a2d37ad09fcd357b182d684fafc",
            "computerDnsName": "ComputerPII_2ea21b2d97c9df23c143ad9e3e454cb674232529.DomainPII_21eed80b086e79bdfa178eabfa25e8be9acfa346.corp.contoso.com",
            "osPlatform": "WindowsServer2016",
            "rbacGroupName": "UnassignedGroup",

        },
        {
            "id": "3d9b1ca53e8f077199c7dcbfc9dbfa78f9bf1918",
            "computerDnsName": "ComputerPII_001d606fc149567c192747f48fae304b43c0ddba.DomainxPII_21eed80b086e79bdfa178eabfa25e8be9acfa346.corp.contoso.com",
            "osPlatform": "WindowsServer2012R2",
            "rbacGroupName": "UnassignedGroup",

        },
        {
            "id": "3db8b27e6172951d7ea2e2d75945abec56feaf82",
            "computerDnsName": "ComputerPII_ce60cfbjj4b82a091deb5eae560332bba99a9bd7.DomainPII_0bc1aee0fa396d175e514bd61a9e7a5b2b07ee8e.corp.contoso.com",
            "osPlatform": "WindowsServer2016",
            "rbacGroupName": "UnassignedGroup",

        },
        {
            "id": "3bad326dcda5b53fab47408cd4a7080f3f3cc8ab",
            "computerDnsName": "ComputerPII_b6b35960dd6539d1d1cef5ada02e235e7b357408.DomainPII_21eed80b089e76bdfa178eadfa25e8de9acfa346.corp.contoso.com",
            "osPlatform": "WindowsServer2012R2",
            "rbacGroupName": "UnassignedGroup",

        }
]
}
```

## See also

- [Remediation methods and properties](get-remediation-methods-properties.md)
- [Get one remediation activity by Id](get-remediation-one-activity.md)
- [List all remediation activities](get-remediation-all-activities.md)
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)
- [Vulnerabilities in your organization](/defender-vulnerability-management/tvm-weaknesses)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
