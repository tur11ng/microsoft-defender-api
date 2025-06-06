---
title: Create an app to access Microsoft Defender for Endpoint without a user
ms.reviewer: 
description: Learn how to design a web app to get programmatic access to Microsoft Defender for Endpoint without a user.
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

# Create an app to access Microsoft Defender for Endpoint without a user

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]


**Applies to:** 

- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](/defender-business)

> [!IMPORTANT]
> Advanced hunting capabilities are not included in Defender for Business.


> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

This page describes how to create an application to get programmatic access to Defender for Endpoint without a user. If you need programmatic access to Defender for Endpoint on behalf of a user, see [Get access with user context](exposed-apis-create-app-nativeapp.md). If you are not sure which access you need, see [Get started](apis-intro.md).

Microsoft Defender for Endpoint exposes much of its data and actions through a set of programmatic APIs. Those APIs will help you automate work flows and innovate based on Defender for Endpoint capabilities. The API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

In general, you'll need to take the following steps to use the APIs:
- Create a Microsoft Entra application.
- Get an access token using this application.
- Use the token to access Defender for Endpoint API.

This article explains how to create a Microsoft Entra application, get an access token to Microsoft Defender for Endpoint, and validate the token.

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

## Create an app

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Navigate to **Microsoft Entra ID** \> **App registrations** \> **New registration**. 

    :::image type="content" source="../media/atp-azure-new-app2.png" alt-text="The application registration pane" lightbox="../media/atp-azure-new-app2.png":::

3. In the registration form, choose a name for your application, and then select **Register**.

4. To enable your app to access Defender for Endpoint and assign it **'Read all alerts'** permission, on your application page, select **API Permissions** \> **Add permission** \> **APIs my organization uses** >, type **WindowsDefenderATP**, and then select **WindowsDefenderATP**.

   > [!NOTE]
   > `WindowsDefenderATP` does not appear in the original list. Start writing its name in the text box to see it appear.

   :::image type="content" source="../media/add-permission.png" alt-text="The API permissions pane" lightbox="../media/add-permission.png":::

   Select **Application permissions** \> **Alert.Read.All**, and then select **Add permissions**.

   :::image type="content" source="../media/application-permissions.png" alt-text="The application permission information pane" lightbox="../media/application-permissions.png":::

5. Select appropriate permissions. `Read All Alerts` is only an example. Here are some examples:

   - To [run advanced queries](run-advanced-query-api.md), select the `Run advanced queries` permission.
   - To [isolate a device](isolate-machine.md), select the `Isolate machine` permission.
   - To determine which permission you need, look at the **Permissions** section in the API you are interested to call.

5. Select **Grant consent**.

   > [!NOTE]
   > Every time you add a permission, you must select **Grant consent** for the new permission to take effect.

   :::image type="content" source="../media/grant-consent.png" alt-text="The grant permissions page" lightbox="../media/grant-consent.png":::

6. To add a secret to the application, select **Certificates & secrets**, add a description to the secret, and then select **Add**.

   > [!NOTE]
   > After you select **Add**, select **copy the generated secret value**. You won't be able to retrieve this value after you leave.

   :::image type="content" source="../media/webapp-create-key2.png" alt-text="The create application option" lightbox="../media/webapp-create-key2.png":::

7. Write down your application ID and your tenant ID. On your application page, go to **Overview** and copy the following.

   :::image type="content" source="../media/app-and-tenant-ids.png" alt-text="The created app and tenant IDs" lightbox="../media/app-and-tenant-ids.png":::

8. **For Microsoft Defender for Endpoint Partners only**. Set your app to be multi-tenanted (available in all tenants after consent). This is **required** for third-party apps (for example, if you create an app that is intended to run in multiple customers' tenant). This is **not required** if you create a service that you want to run in your tenant only (for example, if you create an application for your own usage that will only interact with your own data). To set your app to be multi-tenanted, follow these steps:

   1. Go to **Authentication**, and add `https://portal.azure.com` as the **Redirect URI**.

   2. On the bottom of the page, under **Supported account types**, select the **Accounts in any organizational directory** application consent for your multi-tenant app.

      You need your application to be approved in each tenant where you intend to use it. This is because your application interacts Defender for Endpoint on behalf of your customer.

       You (or your customer if you are writing a third-party app) need to select the consent link and approve your app. The consent should be done with a user who has administrative privileges in Active Directory.

       The consent link is formed as follows: 

       ```https
       https://login.microsoftonline.com/common/oauth2/authorize?prompt=consent&client_id=00000000-0000-0000-0000-000000000000&response_type=code&sso_reload=true
       ```

       Where `00000000-0000-0000-0000-000000000000` is replaced with your application ID.


**Done!** You have successfully registered an application! See examples below for token acquisition and validation.

## Get an access token

For more information on Microsoft Entra tokens, see the [Microsoft Entra tutorial](/azure/active-directory/develop/active-directory-v2-protocols-oauth-client-creds).

### Use PowerShell

```powershell
# This script acquires the App Context Token and stores it in the variable $token for later use in the script.
# Paste your Tenant ID, App ID, and App Secret (App key) into the indicated quotes below.

$tenantId = '' ### Paste your tenant ID here
$appId = '' ### Paste your Application ID here
$appSecret = '' ### Paste your Application key here

$sourceAppIdUri = 'https://api.securitycenter.microsoft.com/.default'
$oAuthUri = "https://login.microsoftonline.com/$TenantId/oauth2/v2.0/token"
$authBody = [Ordered] @{
    scope = "$sourceAppIdUri"
    client_id = "$appId"
    client_secret = "$appSecret"
    grant_type = 'client_credentials'
}
$authResponse = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $authBody -ErrorAction Stop
$token = $authResponse.access_token
$token
```

### Use C#:

The following code was tested with NuGet Microsoft.Identity.Client 3.19.8.

> [!IMPORTANT]
> The [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) NuGet package and Azure AD Authentication Library (ADAL) have been deprecated. No new features have been added since June 30, 2020.   We strongly encourage you to upgrade, see the [migration guide](/azure/active-directory/develop/msal-migration) for more details.

1. Create a new console application.

1. Install NuGet [Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client/).

1. Add the following:

    ```csharp
    using Microsoft.Identity.Client;
    ```

1. Copy and paste the following code in your app (don't forget to update the three variables: ```tenantId, appId, appSecret```):

    ```csharp
    string tenantId = "00000000-0000-0000-0000-000000000000"; // Paste your own tenant ID here
    string appId = "11111111-1111-1111-1111-111111111111"; // Paste your own app ID here
    string appSecret = "22222222-2222-2222-2222-222222222222"; // Paste your own app secret here for a test, and then store it in a safe place! 
    const string authority = "https://login.microsoftonline.com";
    const string audience = "https://api.securitycenter.microsoft.com";

    IConfidentialClientApplication myApp = ConfidentialClientApplicationBuilder.Create(appId).WithClientSecret(appSecret).WithAuthority($"{authority}/{tenantId}").Build();

    List<string> scopes = new List<string>() { $"{audience}/.default" };

    AuthenticationResult authResult = myApp.AcquireTokenForClient(scopes).ExecuteAsync().GetAwaiter().GetResult();

    string token = authResult.AccessToken;
    ```

### Use Python

See [Get token using Python](run-advanced-query-sample-python.md#get-token).

### Use Curl

> [!NOTE]
> The following procedure assumes that Curl for Windows is already installed on your computer.

1. Open a command prompt, and set `CLIENT_ID` to your Azure application ID.

1. Set `CLIENT_SECRET` to your Azure application secret.

1. Set `TENANT_ID` to the Azure tenant ID of the customer that wants to use your app to access Defender for Endpoint.

1. Run the following command:

    ```console
    curl -i -X POST -H "Content-Type:application/x-www-form-urlencoded" -d "grant_type=client_credentials" -d "client_id=%CLIENT_ID%" -d "scope=https://securitycenter.onmicrosoft.com/windowsatpservice/.default" -d "client_secret=%CLIENT_SECRET%" "https://login.microsoftonline.com/%TENANT_ID%/oauth2/v2.0/token" -k
    ```
    
    You get an answer that resembles the following code snippet:
    
    ```console
    {"token_type":"Bearer","expires_in":3599,"ext_expires_in":0,"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIn <truncated> aWReH7P0s0tjTBX8wGWqJUdDA"}
    ```
    
## Validate the token

Ensure that you got the correct token:

1. Copy and paste the token you got in the previous step into [JWT](https://jwt.ms) in order to decode it.

1. Validate that you get a roles claim with the desired permissions.

   In the following image, you can see a decoded token acquired from an app with permissions to all of  Microsoft Defender for Endpoint's roles:

   :::image type="content" source="../media/webapp-decoded-token.png" alt-text="The token details portion" lightbox="../media/webapp-decoded-token.png":::

## Use the token to access Microsoft Defender for Endpoint API

1. Choose the API you want to use. For more information, see [Supported Defender for Endpoint APIs](exposed-apis-list.md).

1. Set the authorization header in the `http` request you send to `Bearer {token}` (Bearer is the authorization scheme).

1. The expiration time of the token is one hour. You can send more than one request with the same token.

The following is an example of sending a request to get a list of alerts **using C#**:

```csharp
var httpClient = new HttpClient();

var request = new HttpRequestMessage(HttpMethod.Get, "https://api.securitycenter.microsoft.com/api/alerts");

request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", token);

var response = httpClient.SendAsync(request).GetAwaiter().GetResult();

// Do something useful with the response
```

## See also

- [Supported Microsoft Defender for Endpoint APIs](exposed-apis-list.md)
- [Access Microsoft Defender for Endpoint on behalf of a user](exposed-apis-create-app-nativeapp.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
