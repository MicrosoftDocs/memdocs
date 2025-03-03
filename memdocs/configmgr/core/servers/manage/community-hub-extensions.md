---
title: Console extensions from Community hub
titleSuffix: Configuration Manager
description: Learn about managing Community hub console extensions for Configuration Manager
ms.date: 10/31/2022
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: how-to
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Console extensions from Community hub

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in March 2023, this feature of Configuration Manager is being removed. 
All future versions, starting with 2303 will not have the Community hub node in the admin console. The Community hub node in older versions will be redirected to [deprecated features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

When you use Configuration Manager version 2103 or later, you can download console extensions from the [Community hub](community-hub.md) and have it applied to all consoles connected to a hierarchy. The **Console extensions** node allows you to start managing the approval and installation of console extensions used in your environment. Getting an extension from community hub doesn't make it immediately available. First, an administrator has to approve the extension for the site. Then console users can install the extension to their local console.

After you approve an extension, when you open the console, you'll see a [console notification](#bkmk_notification). From the notification, you can start the extension installer. After the installer completes, the console restarts automatically, and then you can use the extension. <!--3555909-->

## Find extensions in Community hub

Extensions in Community hub are recognizable by their icon. When browsing **All objects** in the Community hub, you can easily notice if a new extension has been added.The following icon is used for extensions:

:::image type="content" source="media/3555909-extension-icon.png" alt-text="Screenshot of the extension icon used in Community hub. A teal square is surrounded by a broken outline of a square in gray and purple.":::

You can also use a search filter to find an extension in Community hub. Start with the search filter for `type:extension`, then add additional filters as needed.  If you're not finding an extension that's known to be available, double check the [displayed categories hierarchy setting](community-hub.md#bkmk_category) for Community hub.  

[!INCLUDE [Community hub search filters](includes/community-hub-search-filter.md)]

## Download and deploy the extension

You'll download the extension from Community hub, then use the **Console Extensions** node to test the extension and deploy it to other Configuration Manager console users. In-depth instructions for the deployment process and managing extensions can be found in the [Console Extensions](admin-console-extensions.md) article. Below is a high-level overview of the extension deployment process: 

1. Once you've found an extension in Community hub that you want in your environment, select **Download**.
1. The downloaded extension will appear in the [**Console Extensions**](admin-console-extensions.md) node.
1. Change the security scope for the extension, approve it, then install and test it on a local console. For more information on this process, see [Install and test an extension on a local console](admin-console-extensions.md#bkmk_local_install).
1. When testing is complete, [enable user notifications](admin-console-extensions.md#bkmk_enable-notifications) for installation.

## <a name="bkmk_notification"></a> Console extension installation notifications
<!--3555909-->

[!INCLUDE [console extensions notifications](includes/console-extensions-notifications.md)]

## Next steps

- [Manage console extensions](admin-console-extensions.md)
- [Import console extensions](import-admin-console-extensions.md)
- [Create and contribute your own console extension](../../../develop/core/servers/console/console-extension-register.md)
