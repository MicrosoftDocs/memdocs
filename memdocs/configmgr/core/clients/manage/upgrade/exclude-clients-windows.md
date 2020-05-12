---
title: Exclude client upgrades for Windows
titleSuffix: Configuration Manager
description: Learn how to exclude Windows clients from getting upgraded in Configuration Manager.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# How to exclude clients from upgrade in Configuration Manager

*Applies to: Configuration Manager (current branch)*

You can exclude a collection of clients from automatically installing updated client versions. Use this exclusion for a collection of computers that need greater care when upgrading the client. A client that's in an excluded collection ignores requests to install updated client software.

This exclusion applies to the following methods:

- Automatic upgrade
- Software update-based upgrade
- Logon scripts
- Group policy

> [!NOTE]
> Although the user interface states that clients won't upgrade via any method, there are two methods you can use to override these settings. Use client push or manual client installation to override this configuration. For more information, see [How to upgrade an excluded client](#bkmk_override).

## <a name="bkmk_exclude"></a> Configure exclusion

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, select the **Sites** node, and then select **Hierarchy Settings** in the ribbon.

2. Switch to the **Client Upgrade** tab.

3. Select the option to **Exclude specified clients from upgrade**. Then select the **Exclusion collection** you want to exclude. You can only select a single collection for exclusion.

4. Select **OK** to close and save the configuration.

![Settings for automatic upgrade exclusion](media/automatic_upgrade_exclusion.png)

After clients in the excluded collection update policy, they don't automatically install client updates. For more information, see [How to upgrade clients for Windows computers](upgrade-clients-for-windows-computers.md).

> [!NOTE]
> Excluded clients still download and run Ccmsetup, but don't upgrade.

When you remove a client from the exclude collection, it doesn't automatically upgrade until the next auto-upgrade cycle.

## <a name="bkmk_override"></a> How to upgrade an excluded client

If a device is a member of a collection that you excluded from upgrade, you can still upgrade the client using one of the following methods:

- **Client push installation**: Ccmsetup allows client push installation because it's your direct intent. This method lets you upgrade a client without removing it from the collection, or removing the entire collection from exclusion.

- **Manual client installation**: Manually upgrade an excluded client by using the following Ccmsetup command-line parameter: **/IgnoreSkipUpgrade**

    If you attempt to manually upgrade a client that's a member of the excluded collection, and don't use this parameter, the client doesn't upgrade. For more information, see [How to install Configuration Manager clients manually](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

## See also

- [Upgrade clients](upgrade-clients.md)

- [How to deploy clients to Windows computers](../../deploy/deploy-clients-to-windows-computers.md)

- [Extended interoperability client](../../../understand/interoperability-client.md)
