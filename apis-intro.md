---
title: Access the Microsoft Defender for Endpoint APIs
ms.reviewer:
description: Learn how you can use APIs to automate workflows and innovate based on Microsoft Defender for Endpoint capabilities
ms.service: defender-endpoint
ms.subservice: reference
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
ms.custom: api
search.appverid: met150
---

# Access the Microsoft Defender for Endpoint APIs

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> [!IMPORTANT]
> Advanced hunting capabilities are not included in Defender for Business. 

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

Defender for Endpoint exposes much of its data and actions through a set of programmatic APIs. Those APIs will enable you to automate workflows and innovate based on Defender for Endpoint capabilities. The API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

Watch this video for a quick overview of Defender for Endpoint's APIs.

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=f6300637-b48e-49d7-aa76-2778a711ae6c]

In general, you'll need to take the following steps to use the APIs:

- Create a [Microsoft Entra application](exposed-apis-create-app-nativeapp.md)
- Get an access token using this application
- Use the token to access Defender for Endpoint API

You can access Defender for Endpoint API with **Application Context** or **User Context**.

- **Application Context: (Recommended)**

  Used by apps that run without a signed-in user present. for example, apps that run as background services or daemons.

  Steps that need to be taken to access Defender for Endpoint API with application context:

  1. Create a Microsoft Entra Web-Application.
  2. Assign the desired permission to the application, for example, 'Read Alerts', 'Isolate Machines'.
  3. Create a key for this Application.
  4. Get token using the application with its key.
  5. Use the token to access the Microsoft Defender for Endpoint API

     For more information, see [Get access with application context](exposed-apis-create-app-webapp.md).

- **User Context:**

  Used to perform actions in the API on behalf of a user.

  Steps to take to access Defender for Endpoint API with user context:

  1. Create Microsoft Entra Native-Application.
  2. Assign the desired permission to the application, e.g 'Read Alerts', 'Isolate Machines' etc.
  3. Get token using the application with user credentials.
  4. Use the token to access the Microsoft Defender for Endpoint API

     For more information, see [Get access with user context](exposed-apis-create-app-nativeapp.md).


>[!TIP]
>When more than one query request is required to retrieve all the results, Microsoft Graph returns an `@odata.nextLink` property in the response that contains a URL to the next page of results. For more information, see [Paging Microsoft Graph data in your app](/graph/paging).


## Related topics

- [Microsoft Defender for Endpoint APIs](exposed-apis-list.md)
- [Access Microsoft Defender for Endpoint with application context](exposed-apis-create-app-webapp.md)
- [Access Microsoft Defender for Endpoint with user context](exposed-apis-create-app-nativeapp.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
