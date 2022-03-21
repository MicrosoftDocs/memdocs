---
title: Upgrade clients on Windows
titleSuffix: Configuration Manager
description: Upgrade clients on Windows computers in Configuration Manager.
ms.date: 08/23/2021
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# How to upgrade clients for Windows computers in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Upgrade the Configuration Manager client on Windows computers using client installation methods or the automatic client upgrade feature. The following client installation methods are valid ways to upgrade client software on Windows computers:

- Group policy installation

- Logon script installation

- Manual installation

- Upgrade installation

For more information, see [How to deploy clients to Windows computers](../../deploy/deploy-clients-to-windows-computers.md).

Exclude clients from upgrade by specifying an exclusion collection. For more information, see [How to exclude clients from upgrade](exclude-clients-windows.md). Excluded clients still download and run CCMSETUP, but won't upgrade.

> [!TIP]
> If upgrade your server infrastructure from a previous version of Configuration Manager, complete the server upgrades before upgrading the Configuration Manager clients. This process includes installing all current branch updates. The latest current branch update contains the latest version of the client. Upgrade clients after you have installed all of the Configuration Manager updates.

> [!NOTE]
> If you plan to reassign the site for the clients during upgrade, specify the new site using the `SMSSITECODE` client.msi property. If you use the value of `AUTO` for the `SMSSITECODE`, also specify `SITEREASSIGN=TRUE`. This property allows for automatic site reassignment during upgrade. For more information, see [Client installation properties - SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="bkmk_autoupdate"></a> About automatic client upgrade

Configure the site to automatically upgrade clients to the latest Configuration Manager version. When Configuration Manager identifies an assigned client's version is earlier than the hierarchy version, it automatically upgrades the client. This scenario includes upgrading the client to the latest version when it attempts to assign to a Configuration Manager site.

A client can automatically upgrade in the following scenarios:

- The client version is earlier than the version used in the hierarchy.

- The client on the central administration site (CAS) has a language pack installed and the existing client doesn't.

- A client prerequisite in the hierarchy is a different version than the one installed on the client.

- One or more of the client installation files are a different version.

> [!NOTE]
> To identify the different versions of the Configuration Manager client in your hierarchy, use the report **Count of Configuration Manager clients by client versions** in the report folder **Site - Client Information**.

Configuration Manager creates an upgrade package by default. It automatically sends the package to all distribution points in the hierarchy. If you make changes to the client package on the CAS, Configuration Manager automatically updates the package, and redistributes it. An example change is when you add a client language pack. If you enable automatic client upgrade, every client automatically installs the new client language package.

Enable automatic client upgrade across your hierarchy. This configuration keeps your clients up to date with less effort.

If you also manage your Configuration Manager site systems as clients, determine whether to include them as part of the automatic upgrade process. You can exclude all servers, or a specific collection from client upgrade. Some Configuration Manager site roles share the client framework. For example, the management point and pull distribution point. These roles upgrade when you update the site, so the client version on these servers updates at the same time.

## <a name="bkmk_configure"></a> Configure automatic client upgrade

Use the following procedure to configure automatic client upgrade at the CAS. This configuration applies to all clients in your hierarchy.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and then select the **Sites** node.

1. On the **Home** tab of the ribbon, in the **Sites** group, select **Hierarchy Settings**.

1. Switch to the **Client Upgrade** tab. Review the version and date of the production client. Make sure it's the version you want to use to upgrade your clients. If it's not the client version you expect, you may need to promote the pre-production client to production. For more information, see [How to test client upgrades in a pre-production collection](test-client-upgrades.md).

1. Select **Upgrade all clients in the hierarchy using the production client**. Select **OK** to confirm.

1. If you don't want client upgrades to apply to servers, select **Do not upgrade servers**.

1. Specify the number of days in which devices must upgrade the client. After the device receives policy, it upgrades the client at a random interval within this number of days. This behavior prevents a large number of clients simultaneously upgrading.

    > [!NOTE]
    > A computer must be running to upgrade the client. If a computer isn't running when it's scheduled to receive the upgrade, the upgrade doesn't occur. When the computer turns on, and it receives policy, it schedules the upgrade for a random time within the allowed number of days. If this occurs after the number of days to upgrade has expired, it schedules the upgrade at a random time within 24 hours after the computer was turned on.
    >
    > Because of this behavior, computers that are routinely shut down may take longer to upgrade than expected if the randomly scheduled upgrade time isn't within the normal working hours.

1. To exclude clients from upgrade, select **Exclude specified clients from upgrade**, and specify the collection to exclude. For more information, see [Exclude clients from upgrade](exclude-clients-windows.md).

1. If you want the site to copy the client installation package to distribution points that you've enabled for [prestaged content](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent), select the option to **Automatically distribute client installation package to distribution points that are enabled for prestaged content**.

1. Select **OK** to save the settings and close Hierarchy Settings Properties.

Clients receive these settings when they next download policy.

> [!NOTE]
> Client upgrades honor any Configuration Manager maintenance windows you've configured. The ClientServicing thread only runs the client setup bootstrap program (ccmsetup.exe) during a maintenance window. If the device runs an edition of Windows with a write filter, ccmsetup tries to download and install at the same time. Otherwise, ccmsetup randomizes a time to download content. After it downloads content and compiles the local policy, ClientServicing schedules the client upgrade during the next maintenance window.<!-- SCCMDocs#896, MEMDocs#1920 -->

## Next steps

For alternative methods to upgrade clients, see [How to deploy clients to Windows computers](../../deploy/deploy-clients-to-windows-computers.md).

Exclude specific clients from automatic upgrade. For more information, see [How to exclude clients from upgrade](exclude-clients-windows.md).
