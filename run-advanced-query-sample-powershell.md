---
title: Advanced Hunting with PowerShell API Basics
ms.reviewer: 
description: Learn the basics of querying the Microsoft Defender for Endpoint API, using PowerShell.
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
ms.date: 06/19/2024
---

# Advanced Hunting using PowerShell

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:** 
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

Run advanced queries using PowerShell. For more information, see [Advanced Hunting API](run-advanced-query-api.md).

In this section, we share PowerShell samples to retrieve a token and use it to run a query.

## Before you begin
You first need to [create an app](apis-intro.md).

## Preparation instructions

- Open a PowerShell window.

- If your policy doesn't allow you to run the PowerShell commands, you can run the following command:

  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy Bypass
  ```

For more information, see [PowerShell documentation](/powershell/module/microsoft.powershell.security/set-executionpolicy).

## Get token

- Run the following:

```powershell
$tenantId = '00000000-0000-0000-0000-000000000000' # Paste your own tenant ID here
$appId = '11111111-1111-1111-1111-111111111111' # Paste your own app ID here
$appSecret = '22222222-2222-2222-2222-222222222222' # Paste your own app secret here

$resourceAppIdUri = 'https://api.securitycenter.microsoft.com'
$oAuthUri = "https://login.microsoftonline.com/$TenantId/oauth2/token"
$body = [Ordered] @{
    resource = "$resourceAppIdUri"
    client_id = "$appId"
    client_secret = "$appSecret"
    grant_type = 'client_credentials'
}
$response = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $body -ErrorAction Stop
$aadToken = $response.access_token
```

Where
- $tenantId: ID of the tenant on behalf of which you want to run the query (that is, the query is run on the data of this tenant)
- $appId: ID of your Microsoft Entra app (the app must have 'Run advanced queries' permission to Defender for Endpoint)
- $appSecret: Secret of your Microsoft Entra app

## Run query

Run the following query:

```powershell
$token = $aadToken
$query = 'DeviceRegistryEvents | limit 10' # Paste your own query here

$url = "https://api.securitycenter.microsoft.com/api/advancedqueries/run"
$headers = @{ 
    'Content-Type' = 'application/json'
    Accept = 'application/json'
    Authorization = "Bearer $aadToken" 
}
$body = ConvertTo-Json -InputObject @{ 'Query' = $query }
$webResponse = Invoke-WebRequest -Method Post -Uri $url -Headers $headers -Body $body -ErrorAction Stop
$response =  $webResponse | ConvertFrom-Json
$results = $response.Results
$schema = $response.Schema
```

- $results contain the results of your query
- $schema contains the schema of the results of your query

### Complex queries

If you want to run complex queries (or multilines queries), save your query in a file and, instead of the first line in the above sample, run the following command:

```powershell
$query = [IO.File]::ReadAllText("C:\myQuery.txt"); # Replace with the path to your file
```

## Work with query results

You can now use the query results.

To output the results of the query in CSV format in file file1.csv, run the following command:

```powershell
$results | ConvertTo-Csv -NoTypeInformation | Set-Content C:\file1.csv
```

To output the results of the query in JSON format in file file1.json, run the following command:

```powershell
$results | ConvertTo-Json | Set-Content file1.json
```


## Related article
- [Microsoft Defender for Endpoint APIs](apis-intro.md)
- [Advanced Hunting API](run-advanced-query-api.md)
- [Advanced Hunting using Python](run-advanced-query-sample-python.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
