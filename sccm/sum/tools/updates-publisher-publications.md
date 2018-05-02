---
title: "Manage publications"
titleSuffix: "Configuration Manager"
description: "Manage groups of software updates as a publication with System Center Updates Publisher"
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
---
# Manage publications in Updates Publisher

*Applies to: System Center Updates Publisher*

You can use publications to manage groups of updates and bundles as a single object. This includes publishing the updates to a management server and exporting the publication as group for use with another install of Updates Publisher.

## Create publications
Publications are created two ways:

-   When you manage updates and bundles in the **Updates Workspace**, you can [assign](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) them to a new publication that is created at that time.

-   In the **Publications Workspace,** you can use the **Create** button on the **Publication** tab of the ribbon. This method lets you create a publication for future use. Later, when you assign updates, you can use this publication.

## Rename a publication
To rename a publication, select the publication from within the **Publications Workspace**, and then on the **Publication** tab of the ribbon, choose **Edit**.

## Change the publication type of updates in a publication
From the **Publication Workspace**, you can modify the **publication type** of updates and bundles that are assigned to a publication.

1. Select the publication that contains the updates you want to modify, and then select one or more update or bundles from the **All &lt;publication name> member updates** list.

2. Next, on the **Home** tab, choose one of the following options. The options that are available depend on the publication type of the updates you have selected.

  -   **Automatic**
  -   **Full Content**
  -   **Metadata only**

After making a change, you might need to refresh the publication view to see the new values.

For information about the different publication types, see [Assign updates and bundles to a publication](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> When you set the publication type of a bundle, all the software updates in that bundle are published with the publication type of that bundle.

## Remove updates from a publication
To remove updates or bundles from a publication, in the **Publications Workspace** select the publication you want to modify, and then select the updates and bundles you want to remove. Next, on the **Home** tab of the ribbon, choose **Remove**.

After updates are removed from a publication, they remain available in the Updates Publisher repository.

## Publish publications
When you publish updates and bundles, Updates Publisher adds information about those updates and bundles (metadata) and possibly the binaries for the updates (full content), to an update server for deployment to devices.

Before you have the option to publish, you must configure the [Update Server](/sccm/sum/tools/updates-publisher-options#update-server) option for Updates Publisher. To open this configuration option, go to **Updates Workspace** &gt; **Overview** and select **Configure WSUS and Signing Certificate.** You can also go to the Update Server page in the Updates Publisher options.

> [!NOTE]   
> Updates Publisher can only publish updates that are 375 megabytes (MB) or less in size.

### To publish a publication

1.  Go to the **Publications Workspace**, and then select a publication that contains the group of updates and bundles that you want to publish or export. Then choose **Publish** from **Home** tab of the ribbon.

2.  On the **Select** page of the **Publish** wizard you can choose to sign all updates with a new publishing certificate, but you cannot change the publication type.

3.  Complete the wizard.

  If publishing fails, you are presented with a link to the UpdatesPublisher.log file that can provide more information.

## Export a publication
You can export a publication from your Updates Publisher repository. Doing so exports the updates and bundles that are assigned to that publication and creates an update catalog. You can then [add](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) and then [import](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) that catalog to another instance of Updates Publisher. You can also [export updates](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates) that are not part of a publication.

To export a publication, go to the **Publications Workspace** and select the publication that contains updates that you want to export. You can only select one publication at a time.

With the publication selected, choose **Export** from the **Home** tab of the ribbon, and then provide a path and filename for the catalog export.

You also have the option to export (include) dependent software updates as part of the export.

## Rename a publication
To rename a publication, select the publication the **Publications Workspace**, and then choose **Edit** from the **Publication** tab of the ribbon.

## Delete a publication
To delete a publication, select the publication the **Publications Workspace**, and then choose **Delete** from the **Publication** tab of the ribbon.

After the publication is removed from Updates Publisher, the updates that were in the publication remain available in the Updates Publisher repository.

## Expire or reactivate updates and bundles
You can use the **Updates Workspace** to select and then expire or reactivate updates and bundles. You can expire and reactivate updates and bundles as many times as you choose.

-   **To expire updates or bundles**, in the Updates Workspace select one or more updates or bundles that are not expired, and then choose **Expire** from the **Home** tab. Until you publish the update or bundle as expired to Configuration Manager, you can reactivate it.

    Before you can remove (delete) a custom update or bundle from Configuration Manager, you must expire it and then publish that expired status to Configuration Manager. After updates or bundles are expired in Configuration Manager, you can no longer deploy or reactivate the update or bundle.

-   **To reactivate updates or bundles**, in the Updates Workspace select one or more updates that are expired, and then choose **Reactivate** from the **Home** tab of the ribbon. If the expired update was previously published as expired to Configuration Manager, you cannot reactivate it.
