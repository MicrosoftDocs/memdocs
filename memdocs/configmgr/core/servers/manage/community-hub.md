---
title: Community hub and GitHub
titleSuffix: Configuration Manager
description: Enable and use Community hub in Configuration Manager
ms.date: 07/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88cead9a-64fe-471e-b57c-81707cefe46c
author: mestew
ms.author: mstewart
manager: dougeby 
---

# Community hub and GitHub
<!--3555935, 3555936-->

The IT Admin community has developed a wealth of knowledge over the years. Rather than reinventing items like Scripts and Reports from scratch, we've built a **Configuration Manager Community hub** where IT Admins can share with each other. By leveraging the work of others, you can save hours of work. The Community hub fosters creativity by building on others work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the Community hub will leverage those tools directly in the Configuration Manager Console as foundational pieces for driving this new community. For the initial release, the content made available in the Community hub will be uploaded only by Microsoft. In the future, IT Admins will be able to upload content on their own, using their own GitHub account.

> [!Note]  
> Community hub is an optional cloud-based feature. It was first introduced in June 2020. For information on how to opt into Community hub, see [Optional features](install-in-console-updates.md#bkmk_options).

## About Community hub

Community hub supports the following objects:

- CMPivot queries
- Applications
- Task sequences
- Configuration items
- PowerShell Scripts
- Reports

## Prerequisites

- The device running the Configuration Manager console used to access the Community hub needs the following items:
   - .NET Framework version 4.6 or higher
   - Windows 10 build 17110 or higher
      - Windows Server isn't supported, so the Configuration Manager console needs to be installed on a Windows 10 device separate from the site server.
   - The logged-in user account can't be the built-in administrator account

- The [administration service](../../../develop/adminservice/set-up.md) in Configuration Manager needs to be set up and functional.

- If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the Configuration Manager console to access internet endpoints. For more information, see [Internet access requirements](../../plan-design/network/internet-endpoints.md#community-hub).

## Permissions

- To import a script: **Create** permission for **SMS_Scripts** class.
- To import a report: Full Administrator security role.


## Use the Community hub

1. Go to the **Community hub** node in the **Community** workspace.
1. Select an item to download.
1. You'll need appropriate permissions in your Configuration Manager site to download objects from the hub and import them into the site.
    - To import a script: **Create** permission for SMS_Scripts class.
    - To import a report: Full Administrator security role.
1. Downloaded reports are deployed to a report folder called **hub** on the reporting services point. Downloaded scripts can be seen in the **Run Scripts** node.
1. View all items downloaded from the hub by your organization by clicking on **Your downloads** from the **Community hub** node.

[![All items downloaded from the community hub](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)

## <a name="bkmk_deeplink"></a> Direct links to Community hub items
<!--4224406-->
*(Introduced in version 2006)*

You can easily navigate to and reference items in the Configuration Manager console Community hub node with a direct link. The intention for this feature is for easier collaboration and being able to share links to Community hub items with your colleagues. Currently, you'll see these links shared by the Configuration Manager team and in the documentation. These deep links are currently only for items in the Community hub node of the console.

For example, use this link to share the [Configure Edge Auto Update script](https://communityhub.microsoft.com/item/7200) (`https://communityhub.microsoft.com/item/7200`). If you have the Configuration Manager 2006 console installed, follow that link, and then select **Launch the Community hub**. The console opens directly to the script in the Community hub.

> [!Note]
> You can't use the the local built-in administrator account when following a Community hub link.


## Next steps

Learn more about creating and using the following objects:

- [Create and run PowerShell scripts](../../../apps/deploy-use/create-deploy-scripts.md)
- [Introduction to reporting](introduction-to-reporting.md)
- [Create and manage task sequences](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)
- [Create and deploy an application](../../../apps/get-started/create-and-deploy-an-application.md)
- [Create configuration items](../../../compliance/deploy-use/create-configuration-items.md)