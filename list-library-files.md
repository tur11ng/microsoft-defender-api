---
title: List library files 
description: Learn how to list live response library files.
search.appverid: met150
ms.service: defender-endpoint
f1.keywords:
- NOCSH
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
ms.date: 03/01/2025
---

#  List library files 

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:** 

- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

[!include[Prerelease information](../../includes/prerelease.md)]

- Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://www.microsoft.com/microsoft-365/windows/microsoft-defender-atp?ocid=docs-wdatp-exposedapis-abovefoldlink) 

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

List live response library files.

## Limitations

1.  Rate limitations for this API are 100 calls per minute and 1,500 calls per
    hour.

## Permissions

One of the following permissions is required to call this API. To learn more,
including how to choose permissions, see [Get
started](apis-intro.md).

|Permission type                       |      Permission          |  Permission display name | 
|-----------------|--------|---------------------------|  
| Application                        | Library.Manage | Manage live response library |
| Delegated (work or school account) | Library.Manage | Manage live response library |

## HTTP request

```HTTP
GET https://api.security.microsoft.com/api/libraryfiles
```

## Request headers

| Name         |      Type                     | Description
|-----------------|--------|---------------------------|
| Authorization   | String | Bearer {token}. Required. |

## Request body
Empty

## Response 
If successful, this method returns 200 - OK response code with a collection
    of live response library file entities.

## Example

**Request**

Here's an example of a request that gets all live response library files.

```HTTP
GET https://api.security.microsoft.com/api/libraryfiles
```

## Response example

Here's an example of the response.

```JSON
HTTP/1.1 200 Ok
Content-type: application/json
{
"\@odata.context": "https://api.security.microsoft.com
/api/\$metadata\#LibraryFiles",
"value": [
    {
    "fileName": "script1.ps1",
    "sha256": "6e212a0db618507c44e4ec8ee7499dfef7e5767e5f8d31144df3b96fd1145caf",
    "description": null,
    "creationTime": "2019-10-24T10:54:23.2009016Z",
    "lastUpdatedTime": "2019-10-24T10:54:23.2009016Z",
    "createdBy": "admin",
    "hasParameters": true,
    "parametersDescription": "test"
    },
    {
    "fileName": "script.sh",
    "sha256": "d0f3e3b0641dbf88ee39c822516e81a909d1d06d22341dd9b1f12aa5e5c027a2",
    "description": null,
    "creationTime": "2018-10-24T11:15:35.3688259Z",
    "lastUpdatedTime": "2018-10-24T11:15:35.3688259Z",
    "createdBy": "username",
    "hasParameters": false
    },
    {
    "fileName": "memdump.exe",
    "sha256": "fa70b87730290c0d30fe255d1dfb65de82f96286ebfeeb1d88ed3cc831329825",
    "description": "Process memory dump",
    "creationTime": "2018-10-24T10:54:23.2009016Z",
    "lastUpdatedTime": "2018-10-24T10:54:23.2009016Z",
    "createdBy": "admin",
    "hasParameters": false
    }
]
}
```


## Related article
- [Run live response](run-live-response.md) 
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
