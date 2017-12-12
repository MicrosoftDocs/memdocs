---
title: "Manage updates"
titleSuffix: "Configuration Manager"
description: "Manage the udpates you deploy and create with System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
caps.latest.revision: 1
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
---
# Manage software updates in Updates Publisher

*Applies to: System Center Updates Publisher*     

In System Center Updates Publisher, you use the **Updates Workspace** to manage
software updates and bundles that you have imported to the repository.  

Management tasks include duplicating, editing, and expiring or reactivating updates and bundles, and assigning updates and bundles to publications. You can also export custom catalogs for use with other Updates Publisher installations.

To get updates that you can manage:
-  [Add an update catalog](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) to your installation of Updates Publisher
-  [Import](/sccm/sum/tools/updates-publisher-catalogs#import-updates) the updates from that catalog to your repository.

You can also [create your own updates](/sccm/sum/tools/create-updates-with-updates-publisher).



## Create a duplicate of an update
You can create duplicates, or copies, of updates that are in your repository. Then you can modify the copy instead of modifying the original update. You cannot create copies of update bundles.

To create a copy, select an update in the **Updates Workspace**, and then choose **Duplicate**. The copy of the update appears in the same location in the Updates Workspace with *Copy of* added to its name.

A new copy you create has a status of **Unexpired**, but otherwise retains the settings of the original.

## Edit updates and bundles
You can select updates and bundles that are in your repository to modify them.

In the **Updates Workspace** select an update or bundle, and then select **Edit** from the **Home** tab to open the edit wizard. Updates and bundles each have separate but closely related wizards that present the same options as the [Create Update](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard) or [Create Bundle](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard) wizards.

When editing, you can change any available detail about the update or bundle so that it can be used in your environment. For example, you can edit the applicability or precedence rules, or change the language. You can also change the product and vendor to move the update or bundle to a custom folder to group updates for your own use.

## Assign updates and bundles to a publication
You can select updates and bundles in the **Updates Workspace** and then choose **Assign** from the **Home** tab of the ribbon to add them to a publication. This starts the **Assign Software Updates** wizard.
-  See [Publish updates and bundles](#publish-updates-and-bundles-from-the-updates-workspace) for information on how to select and publish updates and bundles as a single task.
-  See [Manage publications](/sccm/sum/tools/updates-publisher-publications) for information on how to manage groups of updates and bundles as a single object. After you assign updates to a publication, you can manage that publication, which in turn includes all its assigned updates.

When you assign updates to a publication:

-   You can include expired and non-expired updates and bundles in the same publication.

-   Specify the publication type:

    -   **Full Content** – This publishes the full content of the update to your WSUS Server. This includes metadata and the update binaries.

    -   **Metadata only** – This publishes only the metadata; update binaries are not published. You might choose this option when you want to gather compliance data.

    -   **Automatic** – This mode is only available when you have connected Updates Publisher to Configuration Manager (See the [ConfigMgr Server](/sccm/sum/tools/updates-publisher-options#configmgr-server) option.)

    With this type, Updates Publisher queries Configuration Manager to determine if the updates or bundles should be published with full content or only metadata. Full content for an update is published only when that update meets the **Requested client count threshold** and **Package source size threshold,** which are specified on the **ConfigMgr Server** page of Updates Publisher options.

-   Select a publication:

    -   Use **Assign software update to existing publications** when you have already created a publication that you want to use. This option is not available until at least one publication exists.

    -   Use **Assign software update to a new publication** when you do not have a suitable publication. This will create a new publication with the name that you specify.

After you assign updates to a publication, you can use the **Publication Workspace** to [publish](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) or [export](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation) the publication as a group.

## Publish updates and bundles from the Updates Workspace
When you publish updates and bundles, Updates Publisher adds information about those updates and bundles (metadata) and possibly the binaries for the updates (full content), to an update server for deployment to devices.

Before you have the option to publish, you must configure the [Update Server](/sccm/sum/tools/updates-publisher-options#update-server) option for Updates Publisher. To open this configuration option, go to **Updates Workspace** &gt; **Overview** and select **Configure WSUS and Signing Certificate.** You can also go to the Update Server page in the Updates Publisher options.

There are two ways to publish updates and bundles:
-   Directly from the Updates Workspace. (See the following procedure, *To publish updates and bundles*.)
-   As a [publication](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) from the Publications Workspace.  

> [!NOTE]   
> Updates Publisher can only publish updates that are 375 megabytes (MB) or less in size.

### To publish updates and bundles
1.  Go to **Updates Workspace** and select one or more updates and bundles that you want to publish. Then choose **Publish** from **Home** tab of the ribbon.

2.  On the **Select** page of the **Publish** wizard, select how you want to publish the updates. The options are the same as for [assigning updates](#assign-updates-and-bundles-to-a-publication): **Full Content**, **Metadata only**, or **Automatic**.

    You can also choose to sign all updates with a new publishing certificate.

3.  Complete the wizard.

If publishing fails, you are presented with a link to the UpdatesPublisher.log file that can provide more information.

## Export updates
You can export updates and bundles from your Updates Publisher repository to create a custom update catalog. Then, you can [add](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) and then [import](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) that catalog to another instance of Updates Publisher. (You can also [export updates as a publication](/sccm/sum/tools/updates-publisher-publications##export-a-publication).)

To export directly, go to **Updates Workspace** > **All Software Updates** and select one or more updates and bundles. You cannot export a vendor or product folder, but you can select a folder and then select the updates in that folder for export.

With one or more updates selected, choose **Export** from the **Home** tab of the ribbon, and then provide a path and filename for the catalog export.

You will have the option to export (include) dependent software updates.

## Delete updates and bundles
You can delete updates and bundles of updates to remove them from the Updates Publisher repository.

Go to **Updates Workspace** > **All Software Updates** and select one or more individual updates. Then choose **Delete** from the **Home** tab of the ribbon.

-   If your selection contains only updates or bundles that have not been published or that are expired, you are asked to confirm deletion before they are removed.

-   If your selection includes an update or bundle that has been published and is not yet expired, you are given a warning. You should [expire](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles) those updates and then publish that change before you delete them from the repository.  

If you delete an update or bundle from a vendor and then import that catalog again, that update is restored to your repository.

## Manage vendor and product folders
To view a list of vendors, and products for each vendor for which you have imported or created updates, go to **Updates Workspace** > **Overview** > **All Software Updates**.

Folders for vendors and products are automatically created by Updates Publisher when you use a wizard to import or create a software update or bundle. You can also create these folders manually.

-   To create a vendor folder, in the navigation pane of the **Updates Workspace**,  right-click on **All Software Updates**, and then choose **Create Vendor**.

-   To create a product folder under a vendor folder, right-click on the vendor folder and choose **Create Product**.

In addition to creating folders, you can rename or delete any vendor or product folder in your repository. To do so, right-click on the folder and choose the option you want, **Rename** or **Delete**. Deleting a folder removes all the updates and bundles in that folder and its product folders from the Updates Publisher repository.

You can move updates between vendor and product folders, including to folders you create. To move an update or bundle to a new folder, you must select and then **Edit** the update or bundle. Then, on the **Information** page of the Edit Update wizard you can reassign the vendor and product. When the **Edit Update** wizard completes, the change applies and the update moves to the new folder.

## View the XML of an update or bundle
You can select a single update or bundle in the **Updates Workspace** and then choose **View** XML to display the XML structure of that update. There are no options to edit the XML structure directly.
