---
title: "Updates Publisher"
titleSuffix: "Configuration Manager"
description: "Use System Center Updates Publisher to manage custom updates"
ms.date: 6/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---
# System Center Updates Publisher

*Applies to: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) is a stand-alone tool that enables independent software vendors or line-of-business application developers to manage custom updates. This custom updates management includes updates that have dependencies, like drivers and update bundles.

Using Updates Publisher, you can:

-   Import updates from external catalogs (non-Microsoft update catalogs).
-   Modify update definitions including applicability, and deployment metadata.
-   Export updates to external catalogs.
-   Publish updates to an update server.

After you publish updates to an update server, you can then use System Center Configuration Manager to detect and deploy those updates to your managed devices.

> [!TIP]  
> The previous version, [System Center Updates Publisher 2011](https://go.microsoft.com/fwlink/?LinkId=848111), remains in support. This updated version retains the same functionality, but supports additional operating systems, new features to simplify some tasks, and has an updated user interface.

## Workspaces
When you open Updates Publisher, it defaults to the Overview node of the *Updates Workspace.*

![Updates Publisher console](media/console1.png)   


Updates Publisher has four workspaces to help organize it.


**Updates Workspace:** Use this workspace to [create](/sccm/sum/tools/create-updates-with-updates-publisher) and [manage](/sccm/sum/tools/manage-updates-with-updates-publisher) software updates and update bundles. This workspace includes assigning updates and bundles to a publication, publishing, and exporting to another Updates Publisher repository.

**Publications Workspace:** This workspace is where you [manage publications](/sccm/sum/tools/updates-publisher-publications). A publication is group of updates you create to simplify the export and publishing of the updates.

Managing publications includes publishing updates to a server so your clients can find and install them, exporting updates and bundles for use by other Updates Publisher installations, or modifying the contents of or details of a publication.

**Rules Workspace:** Here is where you [manage applicability rules](/sccm/sum/tools/updates-publisher-applicability-rules) that can be saved and then used with updates you deploy. There are two types of rules:

-   Installable rules – These rules help determine if a client should install an update.
-   Installed rules – These rules verify if an update is already installed.

**Catalogs Workspace:** Use this workspace to add and [manage software update catalogs](/sccm/sum/tools/updates-publisher-catalogs). This workspace includes the import of software updates from those catalogs to the Updates Publisher repository.

## What's new in the System Center Updates Publisher preview

>[!NOTE] 
>The information in this section applies only to the preview version of System Center Updates publisher. To install the preview, download it from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=58390).

There's a new authoring mode in the preview for System Center Updates Publisher to help you author your updates. When you enable authoring mode, a **Categories Workspace** is added to the start screen. A new **Detectoid** button is also added to the **Updates Workspace** when authoring mode is enabled. 

### To enable authoring mode in the preview

1. In upper left corner of the console, click on the **Updates Publisher** **Properties** tab, and then choose **Options**.
1. Go to the **Authoring** options.
1. Check the box for **Enable authoring mode**.

![Enable authoring mode for Updates Publisher](media/scup-enable-authoring-mode.png)

### About the categories workspace

The categories workspace enables update authors to organize updates that belong together. For instance, if you're an OEM, you might wish to organize your updates based on models or product lines. You can define multiple categories and child categories but not grand child categories as you're limited to two levels.

![Screenshot of Categories Workspace](media/scup-categories-workspace.png)

### Assign an update to a category

Once you've authored your update, you can assign it to a category by selecting the update then clicking the **Categorize** button. You can also right-click the update and select **Categorize**.

![Screenshot of categorizing an update](media/scup-categorize-update.png)


### About detectoids

Once authoring mode is enabled, you can create detectoids for updates. Detectoids are useful when you have multiple updates that use the same rule (or a set of rules) to determine applicability. In those instances, you would create a detectoid and assign it as a prerequisite for an update. You can assign multiple detectoids to an authored update.


### Create a detectoid

1. Open the **Updates Workspace**.
1. In the ribbon, click the **Detectoid** button.
1. Follow the prompts in the wizard to create your detectoid.



![Update prerequisites using a detectoid](media/scup-detectoid-as-prerequisite.png)


## Next steps
To get started, first [install](/sccm/sum/tools/install-updates-publisher), and then [configure options](/sccm/sum/tools/updates-publisher-options) for Updates Publisher.
