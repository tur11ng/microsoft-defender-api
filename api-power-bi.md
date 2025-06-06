---
title: Microsoft Defender for Endpoint APIs connection to Power BI
ms.reviewer: yongrhee
description: Create a Power Business Intelligence (BI) report on top of Microsoft Defender for Endpoint APIs.
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
ms.topic: conceptual
ms.subservice: reference
ms.custom: api
search.appverid: met150
ms.date: 03/21/2025
---

# Create custom reports using Power BI

[!INCLUDE [Microsoft Defender XDR rebranding](../../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint](../microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

[!include[Microsoft Defender for Endpoint API URIs for US Government](../../includes/microsoft-defender-api-usgov.md)]

[!include[Improve request performance](../../includes/improve-request-performance.md)]

In this section, you learn to create a Power BI report on top of Defender for Endpoint APIs.

The first example demonstrates how to connect Power BI to Advanced Hunting API, and the second example demonstrates a connection to our OData APIs, such as Machine Actions or Alerts.

## Connect Power BI to Advanced Hunting API

1. Open Microsoft Power BI.

2. Select **Get Data** \> **Blank Query**.

   :::image type="content" source="../media/power-bi-create-blank-query.png" alt-text="The Blank Query option under the Get Data menu item" lightbox="../media/power-bi-create-blank-query.png":::

3. Select **Advanced Editor**.

   :::image type="content" source="../media/power-bi-open-advanced-editor.png" alt-text="The Advanced Editor menu item" lightbox="../media/power-bi-open-advanced-editor.png":::

4. Copy the code snippet below and paste it in the editor:

   ```
       let
           AdvancedHuntingQuery = "DeviceEvents | where ActionType contains 'Anti' | limit 20",
   
           HuntingUrl = "https://api.securitycenter.microsoft.com/api/advancedqueries",
   
           Response = Json.Document(Web.Contents(HuntingUrl, [Query=[key=AdvancedHuntingQuery]])),
   
           TypeMap = #table(
               { "Type", "PowerBiType" },
               {
                   { "Double",   Double.Type },
                   { "Int64",    Int64.Type },
                   { "Int32",    Int32.Type },
                   { "Int16",    Int16.Type },
                   { "UInt64",   Number.Type },
                   { "UInt32",   Number.Type },
                   { "UInt16",   Number.Type },
                   { "Byte",     Byte.Type },
                   { "Single",   Single.Type },
                   { "Decimal",  Decimal.Type },
                   { "TimeSpan", Duration.Type },
                   { "DateTime", DateTimeZone.Type },
                   { "String",   Text.Type },
                   { "Boolean",  Logical.Type },
                   { "SByte",    Logical.Type },
                   { "Guid",     Text.Type }
               }),
   
           Schema = Table.FromRecords(Response[Schema]),
           TypedSchema = Table.Join(Table.SelectColumns(Schema, {"Name", "Type"}), {"Type"}, TypeMap , {"Type"}),
           Results = Response[Results],
           Rows = Table.FromRecords(Results, Schema[Name]),
           Table = Table.TransformColumnTypes(Rows, Table.ToList(TypedSchema, (c) => {c{0}, c{2}}))
   
       in Table
   ```

5. Select **Done**.

6. Select **Edit Credentials**.

   :::image type="content" source="../media/power-bi-edit-credentials.png" alt-text="The Edit Credentials menu item" lightbox="../media/power-bi-edit-credentials.png":::

7. Select **Organizational account** \> **Sign in**.

   :::image type="content" source="../media/power-bi-set-credentials-organizational.png" alt-text="The Sign in option in the Organizational account menu item" lightbox="../media/power-bi-set-credentials-organizational.png":::

8. Enter your credentials and wait to be signed in.

9. Select **Connect**.

   :::image type="content" source="../media/power-bi-set-credentials-organizational-cont.png" alt-text="The sign-in confirmation message in the Organizational account menu item" lightbox="../media/power-bi-set-credentials-organizational-cont.png":::

Now the results of your query appear as a table and you can start to build visualizations on top of it! You can duplicate this table, rename it, and edit the Advanced Hunting query inside to get any data you would like.

## Connect Power BI to OData APIs

The only difference from the previous example and this example is the query inside the editor. 

1. Open Microsoft Power BI.

2. Select **Get Data** \> **Blank Query**.

   :::image type="content" source="../media/power-bi-create-blank-query.png" alt-text="The Blank Query option under the Get Data menu item" lightbox="../media/power-bi-create-blank-query.png":::

3. Select **Advanced Editor**.

   :::image type="content" source="../media/power-bi-open-advanced-editor.png" alt-text="The Advanced Editor menu item" lightbox="../media/power-bi-open-advanced-editor.png":::

4. Copy the following code, and paste it in the editor to pull all **Machine Actions** from your organization:

   ```
       let

           Query = "MachineActions",

           Source = OData.Feed("https://api.securitycenter.microsoft.com/api/" & Query, null, [Implementation="2.0", MoreColumns=true])
       in
           Source
   ```

   You can do the same for **Alerts** and **Machines**. You also can use OData queries for queries filters. See [Using OData Queries](exposed-apis-odata-samples.md).

## Power BI dashboard samples in GitHub

See the [Power BI report templates](https://github.com/microsoft/MicrosoftDefenderATP-PowerBI).

## Sample reports

View the [Microsoft Defender for Endpoint Power BI report samples](/samples/browse/?products=mdatp).

## Related articles

- [Defender for Endpoint APIs](apis-intro.md)
- [Advanced Hunting API](run-advanced-query-api.md)
- [Using OData Queries](exposed-apis-odata-samples.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../../includes/defender-mde-techcommunity.md)]
