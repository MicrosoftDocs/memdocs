---
title: Console extensions for Configuration Manager
titleSuffix: Configuration Manager
description: Learn about managing Configuration Manager console extensions
ms.date: 07/16/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dfda09bc-5eca-4fb6-9064-4e51705cfe58
author: mestew
ms.author: mstewart
manager: dougeby
---

# Manage Configuration Manager console extensions

*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager 2103, the **Console extensions** node allows you to start managing the approval and installation of console extensions used in your environment. Having extensions in the console doesn't make them immediately available. First, an administrator has to approve the extension for the site and enable notifications. Then console users can install the extension to their local console.

After you approve an extension, when you open the console, you'll see a [console notification](#bkmk_notification). From the notification, you can start the extension installer. After the installer completes, the console restarts automatically, and then you can use the extension.

The new style of console extensions have the following benefits:

1. Centralized management of console extensions for the site from the console instead of manually placing binaries on individual consoles.
1. A clear separation of console extensions from different extension providers.
1. The ability for admins to have more control over which console extensions are loaded and used in the environment, to keep them more secure.
1. A hierarchy setting that allows for only using the new style of console extension.
   > [!Important]
   > If this setting is used, your old style extensions that aren't approved through the **Console Extensions** node will no longer be able to be used. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline image](updates.md#bkmk_Baselines). The setting remains `disabled` by default, if you upgraded from a version prior to 2103. If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.

The old style of console extensions may start being phased out in favor of the new style, which is more secure and centrally managed.

[!INCLUDE [console extensions node](includes/console-extensions-node.md)]

## <a name="bkmk_notification"></a> Console extension installation notifications
<!--3555909-->
[!INCLUDE [console extensions notifications](includes/console-extensions-notifications.md)]

## Next steps

- [Console tips](admin-console-tips.md)
- [Configuration Manager console notifications](admin-console-notifications.md)