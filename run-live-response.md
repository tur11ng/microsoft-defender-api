---
title: Run live response commands on a device
description: Learn how to run a sequence of live response commands on a device.
search.appverid: met150
ms.service: defender-endpoint
f1.keywords:
- NOCSH
ms.author: diannegali
author: diannegali
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
ms.date: 04/18/2023
---

# Run live response commands on a device

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)


[!include[Prerelease information](../../includes/prerelease.md)]

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

## API description

Runs a sequence of live response commands on a device

## Limitations

1. Rate limitations for this API are 10 calls per minute (more requests are responded with HTTP 429).

2. 25 concurrently running sessions (requests exceeding the throttling limit receives a "429 - Too many requests" response).

3. If the machine isn't available, the session is queued for up to three days.

4. RunScript command time-outs after 10 minutes.

5. Live response commands can't be queued up and can only be executed one at a time.

6. If the machine that you're trying to run this API call is in an RBAC device group that doesn't have an automated remediation level assigned to it, you need to at least enable the minimum Remediation Level for a given Device Group.
    > [!NOTE]
    > Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.  

7. Multiple live response commands can be run on a single API call. However, when a live response command fails all the subsequent actions won't be executed.

8. Multiple live response sessions can't be executed on the same machine (if live response action is already running, subsequent requests are responded to with HTTP 400 - ActiveRequestAlreadyExists).

> [!NOTE]
> Live response actions initiated from the Device page aren't available in the `machineactions` API.

## Minimum Requirements

Before you can initiate a session on a device, make sure you fulfill the following requirements:

- **Verify that you're running a supported Windows, macOS, or Linux version**.

  Devices must be running one of the following:

  - **Windows 11**
  
  - **Windows 10**
    - [Version 1909](/windows/whats-new/whats-new-windows-10-version-1909) or later
    - [Version 1903](/windows/whats-new/whats-new-windows-10-version-1903) with [KB4515384](https://support.microsoft.com/help/4515384/windows-10-update-kb4515384)
    - [Version 1809 (RS 5)](/windows/whats-new/whats-new-windows-10-version-1809) with [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818)
    - [Version 1803 (RS 4)](/windows/whats-new/whats-new-windows-10-version-1803) with [KB4537795](https://support.microsoft.com/help/4537795/windows-10-update-kb4537795)
    - [Version 1709 (RS 3)](/windows/whats-new/whats-new-windows-10-version-1709) with [KB4537816](https://support.microsoft.com/help/4537816/windows-10-update-kb4537816)

  - **Windows Server 2019 - Only applicable for Public preview**
    - Version 1903 or (with [KB4515384](https://support.microsoft.com/help/4515384/windows-10-update-kb4515384)) later
    - Version 1809 (with [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818))
    
  - **Windows Server 2022**

- **Windows Server 2025**

  - **macOS** [(requires other configuration profiles)](../microsoft-defender-endpoint-mac.md)
      - 13 (Ventura)
      - 12 (Monterey)
      - 11 (Big Sur)

  - **Linux servers**
      - [Supported Linux distributions](../mde-linux-prerequisites.md#supported-linux-distributions)

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Get started](apis-intro.md).

|Permission type|Permission|Permission display name|
|---|---|---|
|Application|Machine.LiveResponse|Run live response on a specific machine|
|Delegated (work or school account)|Machine.LiveResponse|Run live response on a specific machine|

## HTTP request

```HTTP
POST https://api.securitycenter.microsoft.com/API/machines/{machine_id}/runliveresponse
```

## Request headers

|Name|Type|Description|
|---|---|---|
|Authorization|String|Bearer\<token>\. Required.|
|Content-Type|string|application/json. Required.|

## Request body

|Parameter|Type|Description|
|---|---|---|
|Comment|String|Comment to associate with the action.|
|Commands|Array|Commands to run. Allowed values are PutFile, RunScript, GetFile (must be in this order with no limit on repetitions). |

## Commands

|Command Type|Parameters|Description|
|---|---|---|
|PutFile|Key: FileName <p> Value: \<file name\>|Puts a file from the library to the device. Files are saved in a working folder and are deleted when the device restarts by default. NOTE: Doesn't have a response result. |
|RunScript|Key: ScriptName <br> Value: \<Script from library\> <p> Key: Args <br> Value: \<Script arguments\>|Runs a script from the library on a device. <p>  The Args parameter is passed to your script. <p> Time-outs after 10 minutes.|
|GetFile|Key: Path <br> Value: \<File path\>|Collect file from a device. NOTE: Backslashes in path must be escaped.|

## Response

- If successful, this method returns `201 Created`.

- Action entity. If machine with the specified ID wasn't found, you see `404 Not Found`.

## Example

### Request example

Here's an example of the request.

```HTTP
POST https://api.securitycenter.microsoft.com/api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/runliveresponse

```JSON
{
   "Commands":[
      {
         "type":"RunScript",
         "params":[
            {
               "key":"ScriptName",
               "value":"minidump.ps1"
            },
            {
               "key":"Args",
               "value":"OfficeClickToRun"
            }

         ]
      },
      {
         "type":"GetFile",
         "params":[
            {
               "key":"Path",
               "value":"C:\\windows\\TEMP\\OfficeClickToRun.dmp.zip"
            }
         ]
      }
   ],
   "Comment":"Testing Live Response API"
}
```

### Response example

Here's an example of the response.

Possible values for each command status are "Created", "Completed", and "Failed".

```HTTP
HTTP/1.1 200 Ok
```

Content-type: application/json

```JSON
{
    "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineActions/$entity",
    "id": "{machine_action_id}",
    "type": "LiveResponse",
    "requestor": "analyst@microsoft.com",
    "requestorComment": "Testing Live Response API",
    "status": "Pending",
    "machineId": "{machine_id}",
    "computerDnsName": "hostname",
    "creationDateTimeUtc": "2021-02-04T15:36:52.7788848Z",
    "lastUpdateDateTimeUtc": "2021-02-04T15:36:52.7788848Z",
    "errorHResult": 0,
    "commands": [
        {
            "index": 0,
            "startTime": null,
            "endTime": null,
            "commandStatus": "Created",
            "errors": [],
            "command": {
                "type": "RunScript",
                "params": [
                    {
                        "key": "ScriptName",
                        "value": "minidump.ps1"
                    },{
                        "key": "Args",
                        "value": "OfficeClickToRun"
                    }
                ]
            }
        }, {
            "index": 1,
            "startTime": null,
            "endTime": null,
            "commandStatus": "Created",
            "errors": [],
            "command": {
                "type": "GetFile",
                "params": [{
                        "key": "Path", "value": "C:\\windows\\TEMP\\OfficeClickToRun.dmp.zip"
                    }
                ]
            }
        }
    ]
}
```

## Related topics

- [Get machine action API](get-machineaction-object.md)
- [Get live response result](get-live-response-result.md)
- [Cancel machine action](cancel-machine-action.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
