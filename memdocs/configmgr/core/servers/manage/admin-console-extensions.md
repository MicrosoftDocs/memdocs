---
title: Console extensions for Configuration Manager
titleSuffix: Configuration Manager
description: Learn about managing Configuration Manager console extensions
ms.date: 11/19/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Manage Configuration Manager console extensions

*Applies to: Configuration Manager (current branch)*

Starting in Configuration Manager 2103, the **Console extensions** node allows you to start managing the approval and installation of console extensions used in your environment. Having extensions in the console doesn't make them immediately available. First, an administrator has to approve the extension for the site and enable notifications. Then console users can install the extension to their local console.

After you approve an extension, when you open the console, you'll see a [console notification](#bkmk_notification). From the notification, you can start the extension installer. After the installer completes, the console restarts automatically, and then you can use the extension.

The new style of console extensions has the following benefits:

1. Centralized management of console extensions for the site from the console instead of manually placing binaries on individual consoles.
1. A clear separation of console extensions from different extension providers.
1. The ability for admins to have more control over which console extensions are loaded and used in the environment, to keep them more secure.
1. A hierarchy setting that allows for only using the new style of console extension.
   > [!Important]
   > If this setting is used, your old style extensions that aren't approved through the **Console Extensions** node will no longer be able to be used. The setting, **Only allow console extensions that are approved for the hierarchy**, is `enabled` by default if you installed from the [2103 baseline image](updates.md#bkmk_Baselines). The setting remains `disabled` by default, if you upgraded from a version prior to 2103. If the setting was enabled in error, disabling the setting allows the old style extensions to be used again.

The old style of console extensions may start being phased out in favor of the new style, which is more secure and centrally managed.

[!INCLUDE [console extensions node](includes/console-extensions-node.md)]


[!INCLUDE [console extensions local install](includes/console-extensions-local-install.md)]


[!INCLUDE [console extensions enable notification](includes/console-extensions-enable-notification.md)]

[!INCLUDE [Allow unsigned console extensions notifications](includes/console-extensions-allow-unsigned.md)]


## Require installation of a console extension
<!--10486584-->
*(Introduced in 2111)*

Starting in Configuration Manager version 2111, you can require a console extension to be installed before it connects to the site. After you require an extension, it automatically installs for the local console the next time an admin launches it. To require the installation of a console extension:

1. In the Configuration Manager console, go to the **Administration** workspace.
1. Expand **Updates and Servicing** and select the **Console Extensions** node.
1. Select the extension, then select **Require Extension** from either the right-click menu or the ribbon.
   - Selecting **Make Optional** for an extension removes the extension requirement. Console users can still install it locally from the **Console Extensions** node.  
1. The next time the console is launched by a user within the extension's security scope, installation starts automatically.
   - The user launching the console needs local administrator privileges for the extension installation.

## <a name="bkmk_notification"></a> Console extension installation user notifications
<!--3555909-->
[!INCLUDE [console extensions notifications](includes/console-extensions-notifications.md)]

## Status messages for console extensions
<!--11048976-->
*(Introduced in 2111)*

Starting in version 2111, the site creates status messages for events related to console extensions. Status messages improve the visibility and transparency of console extensions that are used with your site. Use these status messages to make sure your site uses known and trusted console extensions. The status messages have IDs from **54201** to **54208**. They all include the following information:

- The user that made the change
- The ID of the extension
- The version of the extension

There are four categories of message events:

- Required or optional
- Approve or disapprove
- Enable or disable
- Tombstone or untombstone

For example, the description of status message ID **54201** is **User `"%1"` made console extension with ID `"%2"` and version `"%3"` required**.

## Next steps

- [Console extensions from Community hub](community-hub-extensions.md)
- [Import console extensions](import-admin-console-extensions.md)
- [Configuration Manager console notifications](admin-console-notifications.md)
- [Console tips](admin-console-tips.md)
