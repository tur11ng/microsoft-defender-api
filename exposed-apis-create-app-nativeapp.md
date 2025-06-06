---
title: Use Microsoft Defender for Endpoint APIs
ms.reviewer:
description: Learn how to design a native Windows app to get programmatic access to Microsoft Defender for Endpoint without a user.
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

# Use Microsoft Defender for Endpoint APIs

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

This page describes how to create an application to get programmatic access to Defender for Endpoint on behalf of a user.

If you need programmatic access Microsoft Defender for Endpoint without a user, refer to [Access Microsoft Defender for Endpoint with application context](exposed-apis-create-app-webapp.md).

If you're not sure which access you need, read the [Introduction page](apis-intro.md).

Microsoft Defender for Endpoint exposes much of its data and actions through a set of programmatic APIs. Those APIs enable you to automate work flows and innovate based on Microsoft Defender for Endpoint capabilities. The API access requires OAuth2.0 authentication. For more information, see [OAuth 2.0 Authorization Code Flow](/azure/active-directory/develop/active-directory-v2-protocols-oauth-code).

In general, you need to take the following steps to use the APIs:

- Create a Microsoft Entra application
- Get an access token using this application
- Use the token to access Defender for Endpoint API

This page explains how to create a Microsoft Entra application, get an access token to Microsoft Defender for Endpoint and validate the token.

> [!NOTE]
> When accessing Microsoft Defender for Endpoint API on behalf of a user, you will need the correct Application permission and user permission.
> If you are not familiar with user permissions on Microsoft Defender for Endpoint, see [Manage portal access using role-based access control](../rbac.md).

> [!TIP]
> If you have the permission to perform an action in the portal, you have the permission to perform the action in the API.

## Create an app

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Navigate to **Microsoft Entra ID** \> **App registrations** \> **New registration**.

   :::image type="content" source="../media/atp-azure-new-app2.png" alt-text="The App registrations page in the Microsoft Azure portal" lightbox="../media/atp-azure-new-app2.png":::

3. When the **Register an application** page appears, enter your application's registration information:
   - **Name** - Enter a meaningful application name that is displayed to users of the app.
   - **Supported account types** - Select which accounts you would like your application to support.

     <br>

     |Supported account types|Description|
     |---|---|
     |**Accounts in this organizational directory only**|Select this option if you're building a line-of-business (LOB) application. This option isn't available if you're not registering the application in a directory. <br/><br/> This option maps to Microsoft Entra-only single-tenant. <br/><br/> This option is the default option unless you're registering the app outside of a directory. In cases where the app is registered outside of a directory, the default is Microsoft Entra multitenant and personal Microsoft accounts.|
     |**Accounts in any organizational directory**|Select this option if you would like to target all business and educational customers. <br/><br/> This option maps to a Microsoft Entra-only multitenant. <br/><br/> If you registered the app as Microsoft Entra-only single-tenant, you can update it to be Microsoft Entra multitenant and back to single-tenant through the **Authentication** blade.|
     |**Accounts in any organizational directory and personal Microsoft accounts**|Select this option to target the widest set of customers. <br/><br/> This option maps to Microsoft Entra multitenant and personal Microsoft accounts. <br/><br/> If you registered the app as Microsoft Entra multitenant and personal Microsoft accounts, you can't change this in the UI. Instead, you must use the application manifest editor to change the supported account types.|

   - **Redirect URI (optional)** - Select the type of app you're building, **Web** or **Public client (mobile & desktop)**, and then enter the redirect URI (or reply URL) for your application.

     - For web applications, provide the base URL of your app. For example, `http://localhost:31544` might be the URL for a web app running on your local machine. Users would use this URL to sign in to a web client application.

     - For public client applications, provide the URI used by Microsoft Entra ID to return token responses. Enter a value specific to your application, such as `myapp://auth`.

     To see specific examples for web applications or native applications, check out our [quickstarts](/azure/active-directory/develop/#quickstarts).

     When finished, select **Register**.

4. Allow your Application to access Microsoft Defender for Endpoint and assign it 'Read alerts' permission:

   - On your application page, select **API Permissions** \> **Add permission** \> **APIs my organization uses** > type **WindowsDefenderATP** and select on **WindowsDefenderATP**.

     > [!NOTE]
     > *WindowsDefenderATP* does not appear in the original list. Start writing its name in the text box to see it appear.

     :::image type="content" alt-text="add permission." source="../media/add-permission.png" lightbox="../media/add-permission.png":::

   - Choose **Delegated permissions** \> **Alert.Read** > select **Add permissions**.

      :::image type="content" source="../media/application-permissions-public-client.png" alt-text="The application type and permissions panes" lightbox="../media/application-permissions-public-client.png":::

   > [!IMPORTANT]
   > Select the relevant permissions. Read alerts is only an example.

     For example:

     - To [run advanced queries](run-advanced-query-api.md), select **Run advanced queries** permission.
     - To [isolate a device](isolate-machine.md), select **Isolate machine** permission.
     - To determine which permission you need, view the **Permissions** section in the API you're interested to call.

   - Select **Grant consent**.

      > [!NOTE]
      > Every time you add permission you must select on **Grant consent** for the new permission to take effect.

      :::image type="content" source="../media/grant-consent.png" alt-text="The Grand admin consent option" lightbox="../media/grant-consent.png":::

5. Write down your application ID and your tenant ID.

    On your application page, go to **Overview** and copy the following information:

    :::image type="content" source="../media/app-and-tenant-ids.png" alt-text="The created app ID"  lightbox="../media/app-and-tenant-ids.png":::

## Get an access token

For more information on Microsoft Entra tokens, see [Microsoft Entra tutorial](/azure/active-directory/develop/active-directory-v2-protocols-oauth-client-creds).

### Using C\#

- Copy/Paste the below class in your application.
- Use **AcquireUserTokenAsync** method with your application ID, tenant ID, user name, and password to acquire a token.

    ```csharp
    namespace WindowsDefenderATP
    {
        using System.Net.Http;
        using System.Text;
        using System.Threading.Tasks;
        using Newtonsoft.Json.Linq;

        public static class WindowsDefenderATPUtils
        {
            private const string Authority = "https://login.microsoftonline.com";

            private const string WdatpResourceId = "https://api.securitycenter.microsoft.com";

            public static async Task<string> AcquireUserTokenAsync(string username, string password, string appId, string tenantId)
            {
                using (var httpClient = new HttpClient())
                {
                    var urlEncodedBody = $"resource={WdatpResourceId}&client_id={appId}&grant_type=password&username={username}&password={password}";

                    var stringContent = new StringContent(urlEncodedBody, Encoding.UTF8, "application/x-www-form-urlencoded");

                    using (var response = await httpClient.PostAsync($"{Authority}/{tenantId}/oauth2/token", stringContent).ConfigureAwait(false))
                    {
                        response.EnsureSuccessStatusCode();

                        var json = await response.Content.ReadAsStringAsync().ConfigureAwait(false);

                        var jObject = JObject.Parse(json);

                        return jObject["access_token"].Value<string>();
                    }
                }
            }
        }
    }
    ```

## Validate the token

Verify to make sure you got a correct token:

- Copy/paste into [JWT](https://jwt.ms) the token you got in the previous step in order to decode it.
- Validate you get a 'scp' claim with the desired app permissions.
- In the screenshot below you can see a decoded token acquired from the app in the tutorial:

  :::image type="content" source="../media/nativeapp-decoded-token.png" alt-text="The token validation page" lightbox="../media/nativeapp-decoded-token.png":::

## Use the token to access Microsoft Defender for Endpoint API

- Choose the API you want to use - [Supported Microsoft Defender for Endpoint APIs](exposed-apis-list.md).
- Set the Authorization header in the HTTP request you send to "Bearer {token}" (Bearer is the Authorization scheme).
- The Expiration time of the token is 1 hour (you can send more than one request with the same token).

- Example of sending a request to get a list of alerts **using C#**:

    ```csharp
    var httpClient = new HttpClient();

    var request = new HttpRequestMessage(HttpMethod.Get, "https://api.securitycenter.microsoft.com/api/alerts");

    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", token);

    var response = httpClient.SendAsync(request).GetAwaiter().GetResult();

    // Do something useful with the response
    ```

## See also

- [Microsoft Defender for Endpoint APIs](exposed-apis-list.md)
- [Access Microsoft Defender for Endpoint with application context](exposed-apis-create-app-webapp.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
