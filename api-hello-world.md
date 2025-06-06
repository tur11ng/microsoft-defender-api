---
title: Hello World for Microsoft Defender for Endpoint API
ms.reviewer:
description: Create a practice 'Hello world'-style API call to the Microsoft Defender for Endpoint API.
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
ms.date: 03/21/2025
---

# Microsoft Defender for Endpoint API - Hello World

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]


**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](../microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]


## Get Alerts using a simple PowerShell script

### How long it takes to go through this example?

It only takes 5 minutes done in two steps:

- Application registration
- Use examples: only requires copy/paste of a short PowerShell script

### Do I need a permission to connect?

For the Application registration stage, you must have an appropriate role assigned in your Microsoft Entra tenant. For more details about roles, see [Permission options](../user-roles.md#permission-options).

<a name='step-1---create-an-app-in-azure-active-directory'></a>

### Step 1 - Create an App in Microsoft Entra ID

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Navigate to **Microsoft Entra ID** \> **App registrations** \> **New registration**.

   :::image type="content" source="../media/atp-azure-new-app2.png" alt-text="The App registrations option under the Manage pane in the Microsoft Entra admin center"  lightbox="../media/atp-azure-new-app2.png":::

3. In the registration form, choose a name for your application and then select **Register**.

4. Allow your Application to access Defender for Endpoint and assign it **'Read all alerts'** permission:

   - On your application page, select **API Permissions** \> **Add permission** \> **APIs my organization uses** > type **WindowsDefenderATP** and select **WindowsDefenderATP**.

     > [!NOTE]
     > WindowsDefenderATP does not appear in the original list. You need to start writing its name in the text box to see it appear.

     :::image type="content" source="../media/add-permission.png" alt-text="The API permissions option under the Manage pane in the Microsoft Entra admin center" lightbox="../media/add-permission.png":::

   - Choose **Application permissions** \> **Alert.Read.All**, and then select **Add permissions**.

     :::image type="content" source="../media/application-permissions.png" alt-text="The permission type and settings panes in the Request API permissions page" lightbox="../media/application-permissions.png":::

     > [!IMPORTANT]
     > You need to select the relevant permissions. **Read All Alerts** is only an example.

     For example:

     - To [run advanced queries](run-advanced-query-api.md), select 'Run advanced queries' permission.
     - To [isolate a machine](isolate-machine.md), select 'Isolate machine' permission.
     - To determine which permission you need, see the **Permissions** section in the API you're interested to call.

5. Select **Grant consent**.

   > [!NOTE]
   > Every time you add permission, you must click on **Grant consent** for the new permission to take effect.

   :::image type="content" source="../media/grant-consent.png" alt-text="The grant permission consent option in the Microsoft Entra admin center" lightbox="../media/grant-consent.png":::

6. Add a secret to the application.

    Select **Certificates & secrets**, add description to the secret and select **Add**.

    > [!IMPORTANT]
    > After click Add, **copy the generated secret value**. You won't be able to retrieve after you leave!

    :::image type="content" source="../media/webapp-create-key2.png" alt-text="The Certificates & secrets menu item in the Manage pane in the Microsoft Entra admin center" lightbox="../media/webapp-create-key2.png":::

7. Write down your application ID and your tenant ID.

   On your application page, go to **Overview** and copy the following:

   :::image type="content" source="../media/app-and-tenant-ids.png" alt-text="The application details pane under the Overview menu item in the Microsoft Entra admin center" lightbox="../media/app-and-tenant-ids.png":::

Done! You've successfully registered an application!

### Step 2 - Get a token using the App and use this token to access the API.

- Copy the following script to PowerShell ISE or to a text editor, and save it as `Get-Token.ps1`.
- Running this script generates a token and saves it in the working folder under the name `Latest-token.txt`.

   ```powershell
   # That code gets the App Context Token and save it to a file named "Latest-token.txt" under the current directory
   # Paste below your Tenant ID, App ID and App Secret (App key).

   $tenantId = '' ### Paste your tenant ID here
   $appId = '' ### Paste your Application ID here
   $appSecret = '' ### Paste your Application secret here

   $resourceAppIdUri = 'https://api.securitycenter.microsoft.com'
   $oAuthUri = "https://login.microsoftonline.com/$TenantId/oauth2/token"
   $authBody = [Ordered] @{
       resource = "$resourceAppIdUri"
       client_id = "$appId"
       client_secret = "$appSecret"
       grant_type = 'client_credentials'
   }
   $authResponse = Invoke-RestMethod -Method Post -Uri $oAuthUri -Body $authBody -ErrorAction Stop
   $token = $authResponse.access_token
   Out-File -FilePath "./Latest-token.txt" -InputObject $token
   return $token
   ```

- Sanity Check:
  - Run the script.
  - In your browser go to: <https://jwt.ms/>.
  - Copy the token (the content of the Latest-token.txt file).
  - Paste in the top box.
  - Look for the "roles" section. Find the _Alert.Read.All_ role.

  :::image type="content" source="../media/api-jwt-ms.png" alt-text="The Decoded Token pane for jwt.ms" lightbox="../media/api-jwt-ms.png":::

### Let's get the Alerts!

- The following script uses `Get-Token.ps1` to access the API and gets alerts for the past 48 hours.
- Save this script in the same folder you saved the previous script `Get-Token.ps1`.
- The script creates two files (json and csv) with the data in the same folder as the scripts.

  ```powershell
  # Returns Alerts created in the past 48 hours.

  $token = ./Get-Token.ps1       #run the script Get-Token.ps1  - make sure you are running this script from the same folder of Get-Token.ps1

  # Get Alert from the last 48 hours. Make sure you have alerts in that time frame.
  $dateTime = (Get-Date).ToUniversalTime().AddHours(-48).ToString("o")

  # The URL contains the type of query and the time filter we create above
  # Read more about [other query options and filters](get-alerts.md).
  $url = "https://api.securitycenter.microsoft.com/api/alerts?`$filter=alertCreationTime ge $dateTime"

  # Set the WebRequest headers
  $headers = @{
      'Content-Type' = 'application/json'
      Accept = 'application/json'
      Authorization = "Bearer $token"
  }

  # Send the webrequest and get the results.
  $response = Invoke-WebRequest -Method Get -Uri $url -Headers $headers -ErrorAction Stop

  # Extract the alerts from the results.
  $alerts =  ($response | ConvertFrom-Json).value | ConvertTo-Json

  # Get string with the execution time. We concatenate that string to the output file to avoid overwrite the file
  $dateTimeForFileName = Get-Date -Format o | foreach {$_ -replace ":", "."}

  # Save the result as json and as csv
  $outputJsonPath = "./Latest Alerts $dateTimeForFileName.json"
  $outputCsvPath = "./Latest Alerts $dateTimeForFileName.csv"

  Out-File -FilePath $outputJsonPath -InputObject $alerts
  ($alerts | ConvertFrom-Json) | Export-CSV $outputCsvPath -NoTypeInformation
  ```

You're all done! You have successfully:

- Created and registered and application
- Granted permission for that application to read alerts
- Connected the API
- Used a PowerShell script to return alerts created in the past 48 hours

## Related articles

- [Microsoft Defender for Endpoint APIs](exposed-apis-list.md)
- [Access Microsoft Defender for Endpoint with application context](exposed-apis-create-app-webapp.md)
- [Access Microsoft Defender for Endpoint with user context](exposed-apis-create-app-nativeapp.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
