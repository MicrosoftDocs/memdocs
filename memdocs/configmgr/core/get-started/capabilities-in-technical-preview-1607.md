---
title: Capabilities in Technical Preview 1607
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview for Configuration Manager, version 1607.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.localizationpriority: medium
---
# Capabilities in Technical Preview 1607 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1607. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## <a name="dmp_edition"></a>Improvements to the Windows 10 Edition Upgrade Policy

In this release, the following improvements have been made to this policy:

* You can now use the edition upgrade policy with Windows 10 PCs that run the Configuration Manager client in addition to Windows 10 PCs are enrolled with Microsoft Intune.
* You can upgrade from Windows 10 Professional to any of the platforms in the wizard that are compatible with your hardware.

[Read more about the Windows 10 Edition Upgrade Policy](../../compliance/deploy-use/upgrade-windows-version.md)

### Try it out!

1. Use the information in the [existing edition upgrade policy topic](../../compliance/deploy-use/upgrade-windows-version.md) to create an edition upgrade policy.
2. Deploy this policy to a Windows 10 PC running the Configuration Manager client.
Once the policy reaches a targeted Windows PC, the PC will be restarted within two hours to apply the upgrade. You cannot currently suppress this restart. Ensure you inform any users to which you deploy the policy, or schedule the policy to run outside of the users working hours.

### Known issue with this release
In Configuration Manager client settings, you might see settings for **Edition Upgrade**. In this release, these settings are not functional. Use the instructions given above to upgrade Windows 10 to a newer version.

## Customizable Branding for Software Center Dialogs

Custom branding for the Software Center was introduced in Configuration Manager version 1602. In Technical Preview version 1607, that branding is now extended to all associated dialog boxes and taskbar notifications to provide a more consistent experience to Software Center users.

### Try it out!

Custom branding for the Software Center is applied according to the following rules:

1. If the Application Catalog website point site server role is not installed, then Software Center will display the organization name specified in the **Computer Agent** client setting **Organization name displayed in Software Center**. For instructions, see [How to configure client settings](../../core/clients/deploy/configure-client-settings.md).

2. If the Application Catalog website point site server role is installed, then Software Center will display the organization name and color specified in the Application Catalog website point site server role properties.

3. If a Microsoft Intune subscription is configured and connected to the Configuration Manager environment, then Software Center will display the organization name, color and company logo specified in the Intune subscription properties.

## Use the same network adapter for multiple PXE initiated deployments
In Technical Preview version 1607, when you use an ethernet adapter to image multiple devices (such as a USB ethernet adapter that you use on multiple devices), you can enable a new setting that allows you to enter hardware identifiers for the ethernet adapters. Configuration Manager ignores the hardware identifiers in the list when performing a PXE installation and for client registration.

For more information about this issue, see the [Configuration Manager OSD Support Team Blog](https://techcommunity.microsoft.com/t5/configuration-manager-archive/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in/ba-p/273721).  

### Enable the feature to manage duplicate hardware identifiers  
1. In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Updates and Servicing** > **Features**.
2. In the display pane, select **Manage duplicate hardware identifiers**.
3. On the **Home** tab, in the **Features** group, click **Turn on**.

### Add hardware identifiers for Configuration Manager to ignore  
1. In the Configuration Manager console, go to **Administration** > **Overview** > **Site Configuration** > **Sites**.
2. On the **Home** tab, in the **Sites** group, click **Hierarchy Settings**.
3. Go to the **Client Approval and Conflicting Records** tab.
4. Click **Add** in the **Duplicate hardware identifiers** section to add new hardware identifiers.
