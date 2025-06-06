---
title: Advanced Hunting API
ms.reviewer:
description: Learn to use the advanced hunting API to run advanced queries on Microsoft Defender for Endpoint. Find out about limitations and see an example.
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

# Advanced hunting API

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
> [!WARNING]
> This advanced hunting API is an older version with limited capabilities. A more comprehensive version of the advanced hunting API that can query more tables is already available in the **[Microsoft Graph security API](/graph/api/resources/security-api-overview)**. See **[Advanced hunting using Microsoft Graph security API](/graph/api/resources/security-api-overview#advanced-hunting)**

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]



## Limitations

1. You can only run a query on data from the last 30 days.

2. The results include a maximum of 100,000 rows.

3. The number of executions is limited per tenant:
   - API calls: Up to 45 calls per minute, and up to 1,500 calls per hour.
   - Execution time: 10 minutes of running time every hour and 3 hours of running time a day.

4. The maximal execution time of a single request is 200 seconds.

5. `429` response represents reaching quota limit either by number of requests or by CPU. Read response body to understand what limit was reached.

6. The maximum query result size of a single request can't exceed 124 MB. If exceeded, an HTTP 400 Bad Request with the message "Query execution has exceeded the allowed result size. Optimize your query by limiting the number of results and try again" occurs.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Use Microsoft Defender for Endpoint APIs](apis-intro.md)

|Permission type|Permission|Permission display name|
|:---|:---|:---|
|Application|AdvancedQuery.Read.All|`Run advanced queries`|
|Delegated (work or school account)|AdvancedQuery.Read|`Run advanced queries`|

> [!NOTE]
> When obtaining a token using user credentials:
>
> - The user needs to have the `View Data` role assigned in Microsoft Entra ID
> - The user needs to have access to the device, based on device group settings (See [Create and manage device groups](../machine-groups.md) for more information)
>
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.  

## HTTP request

```http
POST https://api.securitycenter.microsoft.com/api/advancedqueries/run
```

## Request headers

Header|Value
:---|:---
Authorization|Bearer {token}. **Required**.
Content-Type|application/json

## Request body

In the request body, supply a JSON object with the following parameters:

Parameter|Type|Description
:---|:---|:---
Query|Text|The query to run. **Required**.

## Response

If successful, this method returns 200 OK, and _QueryResponse_ object in the response body.

## Example

### Request example

Here's an example of the request.

```http
POST https://api.securitycenter.microsoft.com/api/advancedqueries/run
```

```json
{
    "Query":"DeviceProcessEvents
|where InitiatingProcessFileName =~ 'powershell.exe'
|where ProcessCommandLine contains 'appdata'
|project Timestamp, FileName, InitiatingProcessFileName, DeviceId
|limit 2"
}
```

### Response example

Here's an example of the response.

> [!NOTE]
> The response object shown here may be truncated for brevity. All of the properties will be returned from an actual call.

```json
{
    "Schema": [
        {
            "Name": "Timestamp",
            "Type": "DateTime"
        },
        {
            "Name": "FileName",
            "Type": "String"
        },
        {
            "Name": "InitiatingProcessFileName",
            "Type": "String"
        },
        {
            "Name": "DeviceId",
            "Type": "String"
        }
    ],
    "Results": [
        {
            "Timestamp": "2020-02-05T01:10:26.2648757Z",
            "FileName": "csc.exe",
            "InitiatingProcessFileName": "powershell.exe",
            "DeviceId": "10cbf9182d4e95660362f65cfa67c7731f62fdb3"
        },
        {
            "Timestamp": "2020-02-05T01:10:26.5614772Z",
            "FileName": "csc.exe",
            "InitiatingProcessFileName": "powershell.exe",
            "DeviceId": "10cbf9182d4e95660362f65cfa67c7731f62fdb3"
        }
    ]
}
```

## Related articles

- [Use the Microsoft Graph security API - Microsoft Graph | Microsoft Learn](/graph/api/resources/security-api-overview)

- [Microsoft Defender for Endpoint APIs introduction](apis-intro.md)
- [Advanced Hunting from Portal](/defender-xdr/advanced-hunting-query-language)
- [Advanced Hunting using PowerShell](run-advanced-query-sample-powershell.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
