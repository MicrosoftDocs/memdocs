---
title: Manage update catalogs
titleSuffix: Configuration Manager
description: Manage software update catalogs for System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# Manage software update catalogs in Updates Publisher

*Applies to: System Center Updates Publisher*

Use the **Catalogs** **Workspace** to manage software update catalogs. This includes adding new catalogs, managing existing catalog subscriptions, and importing information about the updates from a catalog to the Updates Publisher repository.

Software update catalogs contain information about related updates that are created by organizations other than Microsoft. Other organizations include your own organization and third-party software vendors that have registered their catalogs with Microsoft. Registered catalogs from software vendors are called *partner catalogs*. Catalogs that you create, and that are not registered with Microsoft, are called *user* catalogs.

## Add software update catalogs
You must add an update catalog to Updates Publisher before you can manage the updates that it contains. When you add a catalog, Updates Publisher:
-   Creates a subscription to that catalog, so it can check for updates to that catalog.
-   Adds the catalog to a list in the **My Software Update Catalogs** window of the **Catalogs Workspace**.  

Information about each subscribed catalog is available in the console. Information includes the download URL or location, the name of the company or organization who created the catalog, and when it was last imported or modified.

Updates Publisher can automatically check your subscriptions for changes each time it starts. This is configured as an [Advanced option](updates-publisher-options.md#advanced). When configured, Updates Publisher references the download URL or location information for the subscription and alerts you when there are changes to the catalog that were made since the last time you imported it to the repository.

To manually check for a catalog update, select the catalog from the **My Software Update Catalogs** list and then choose **Refresh** from the ribbon.

In addition to adding catalogs, and viewing information about subscribed catalogs, you can:
-  **Edit** information for *user* catalogs.
-  **Delete** (remove) a catalog from Updates Publisher.
-  **Import** updates from a catalog into the Updates Publisher repository. When you import updates, you import all updates contained in that catalog. You can then view the updates in the Updates workspace where you can then select and publish updates to your update server.

> [!NOTE]   
> Deleting a catalog from Updates Publisher results in the updates in that catalog being removed from your repository. This does not affect the updates you have published to your update server. To remove updates from your update server that are no longer in your repository, see [Expire unreferenced software updates](updates-publisher-options.md#expire-unreferenced-software-updates).

## Manage update catalogs
You can view the list catalogs you have imported in the **My Software Update Catalogs** window of the **Catalogs Workspace**. From this workspace you can:

-   **Add a partner catalog:** Use one of the following to find new partner catalogs:

    -   In the console, go to **Updates Workspace** > **Overview**. In the **Getting Started** window, choose **Add Partner Software Updates Catalogs**.

    -   In the console, go to **Catalogs Workspace** > **My Catalogs**. Then, from the ribbon, choose **Add Catalogs**.

-   **Add a user catalog:** In the console, go to **Catalogs Workspace** > **My Catalogs**. Then, from the ribbon, choose **Add Catalogs**. In addition to the location of the .cab file, you must specify a Publisher, Name, and Description to identify the catalog.


-   **Check for updates to catalogs:** Select one or more catalogs and then choose **Refresh** from the ribbon.

-   **Edit a user catalog:** Select a *user* catalog and then choose **Edit** from the ribbon. You can then modify the user defined properties.

-   **Delete catalogs:** Select one or more catalogs and then choose **Remove** from the ribbon. This removes the catalog, your subscription, and the updates from those catalogs from your Updates Publisher repository.

-   **Add updates from a catalog to your repository**: Choose **Import** from the ribbon to start the **Import Catalog** wizard. For more infomration, see [Import updates](#import-updates)

## Import updates
When you import a catalog, Updates Manager adds the updates from that catalog to the Updates Publisher repository. After updates are imported, you can publish them to your update server to make them available to managed devices.

### To import updates
1. To start the **Import Catalog** wizard, choose **Import** from the Ribbon in one of the following workspaces:

   -   Catalogs Workspace

   -   Updates Workspace

2. On the **Import Type** page, select one or more catalogs you've added to Updates Publisher, or specify a path to a catalog you have not yet added as a subscription. Chose **Next** to view the summary screen, and when ready, choose **Next** to start the import.

3. On the **Security Warning – Catalog Validation** window, review the catalog certificate, and when ready, chose **Accept** to import the updates.

   > [!CAUTION]
   > Accept updates only from publishers that you trust. Software updates from publishers who are not trusted can potentially harm client computers when scanning for updates.
   > 
   >  If you no longer trust a publisher, remove that publisher from the trusted publishers list. To find more information about accepting catalogs, click **Tell Me More** in the **Security Warning – Catalog Validation** dialog box.

   If you choose to always accept catalogs from a publisher, that publisher is added to the [trusted publishers list](updates-publisher-options.md#trusted-publishers). You can review and edit this list as an Updates Publisher option.

4. Import skips import of an update when the update is already in the repository and one of the following is true:

   -   The update is unchanged from the last time it was imported.

   -   The update has been edited and has a new digital hash. Editing an update prevents a new update from overwriting the original as doing so would overwrite changes you might have deployed.

5. On the **Confirmation** page review the import results.

6. Click **Close** to complete the wizard. You can now view the updates for this catalog in the Updates Workspace.

## Next steps
After you import updates, common actions include:
-   [Manage updates](manage-updates-with-updates-publisher.md) to bundle, assign, and deploy them your update server.
-   [Create applicability rules](updates-publisher-applicability-rules.md) to help determine when updates deploy to your update server.
