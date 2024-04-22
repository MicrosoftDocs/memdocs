---
title: Configure client settings
titleSuffix: Configuration Manager
description: Learn how to configure client settings in Configuration Manager.
ms.date: 04/05/2021
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: how-to
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to configure client settings in Configuration Manager

*Applies to: Configuration Manager (current branch)*

You manage all client settings in Configuration Manager from  the **Client Settings** node of the **Administration** workspace in the console. When you want to configure settings for all users and devices in the hierarchy, modify the default settings. If you want to apply different settings to just some users or devices, create custom settings and deploy to collections. Custom client settings override the default settings.

For information about each client setting, see [About client settings](about-client-settings.md).

> [!NOTE]
> You can also use configuration items to manage clients to assess, track, and remediate the configuration compliance of devices. For more information, see [Ensure device compliance](../../../compliance/understand/ensure-device-compliance.md).

## Configure default client settings

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.

1. Select **Default Client Settings**. On the **Home** tab of the ribbon, select **Properties**.

1. View and configure the client settings for each group of settings in the navigation pane.

> [!TIP]
> Configuration Manager configures clients with these settings when they next download policy. To start policy retrieval for a single client, see [Start policy retrieval for a Configuration Manager client](../manage/manage-clients.md#start-policy-retrieval).

## Create and deploy custom client settings

When you deploy these custom settings, they override the default client settings. Before you begin this procedure, make sure that you have a collection the deployment. The collection should contain the users or devices that require these custom client settings.

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Custom Client Settings**. Then choose either **Create Custom Client Device Settings** or **Create Custom Client User Settings**.

    1. Specify a unique name and optional description.

    1. Select one or more of the settings groups.

    1. Select each group of settings from the navigation pane, configure the available settings, and then select **OK** to save the settings.

1. Select the custom client setting that you created. On the **Home** tab of the ribbon, in the **Client Settings** group, choose **Deploy**.

1. In the **Select Collection** window, select the appropriate collection, and then choose **OK**. To verify the targeted collection, switch to the **Deployments** tab in the details pane of the **Client Settings** node.

1. View the order of the custom client setting that you created. When you have multiple custom client settings, they're applied according to their order number. If there are any conflicts between settings, the setting that has the lowest order number overrides the other settings. To change the order number, on the **Home** tab of the ribbon, in the **Client Settings** group, choose **Move Item Up** or **Move Item Down**.

> [!TIP]
> Configuration Manage configures clients with these settings when they next download policy. To start policy retrieval for a single client, see [Start policy retrieval for a Configuration Manager client](../manage/manage-clients.md#start-policy-retrieval).

## View client settings

When you deploy multiple client settings to the same device, user, or user group, the prioritization and combination of settings is complex.

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select either the **Devices** or **Users** node.

1. Select a device or user, and in the **Client Settings** group of the ribbon, select **Resultant Client Settings**.

1. Select a client setting from the left pane, and it displays the settings. In this view, the settings are read-only.

    > [!NOTE]
    > To view the client settings, your account needs **Read** access to client settings.

## Automate with PowerShell

Optionally, you can use the Configuration Manager PowerShell cmdlets to automate client settings. For more information, see the following articles in the PowerShell documentation:

- [Get-CMClientSetting](/powershell/module/configurationmanager/Get-CMClientSetting): Get an existing client settings object.

- [New-CMClientSetting](/powershell/module/configurationmanager/New-CMClientSetting): Create a new client settings object.

- [Remove-CMClientSetting](/powershell/module/configurationmanager/Remove-CMClientSetting): Remove a client settings object.

Use the following cmdlets to configure client settings for the specific group:

- [Set-CMClientSettingBackgroundIntelligentTransfer](/powershell/module/configurationmanager/Set-CMClientSettingBackgroundIntelligentTransfer)
- [Set-CMClientSettingClientCache](/powershell/module/configurationmanager/Set-CMClientSettingClientCache)
- [Set-CMClientSettingClientPolicy](/powershell/module/configurationmanager/Set-CMClientSettingClientPolicy)
- [Set-CMClientSettingCloudService](/powershell/module/configurationmanager/Set-CMClientSettingCloudService)
- [Set-CMClientSettingComplianceSetting](/powershell/module/configurationmanager/Set-CMClientSettingComplianceSetting)
- [Set-CMClientSettingComputerAgent](/powershell/module/configurationmanager/Set-CMClientSettingComputerAgent)
- [Set-CMClientSettingComputerRestart](/powershell/module/configurationmanager/Set-CMClientSettingComputerRestart)
- [Set-CMClientSettingDeliveryOptimization](/powershell/module/configurationmanager/Set-CMClientSettingDeliveryOptimization)
- [Set-CMClientSettingEndpointProtection](/powershell/module/configurationmanager/Set-CMClientSettingEndpointProtection)
- [Set-CMClientSettingEnrollment](/powershell/module/configurationmanager/Set-CMClientSettingEnrollment)
- [Set-CMClientSettingGeneral](/powershell/module/configurationmanager/Set-CMClientSettingGeneral)
- [Set-CMClientSettingHardwareInventory](/powershell/module/configurationmanager/Set-CMClientSettingHardwareInventory)
- [Set-CMClientSettingMeteredInternetConnection](/powershell/module/configurationmanager/Set-CMClientSettingMeteredInternetConnection)
- [Set-CMClientSettingPowerManagement](/powershell/module/configurationmanager/Set-CMClientSettingPowerManagement)
- [Set-CMClientSettingRemoteTool](/powershell/module/configurationmanager/Set-CMClientSettingRemoteTool)
- [Set-CMClientSettingSoftwareCenter](/powershell/module/configurationmanager/Set-CMClientSettingSoftwareCenter)
- [Set-CMClientSettingSoftwareDeployment](/powershell/module/configurationmanager/Set-CMClientSettingSoftwareDeployment)
- [Set-CMClientSettingSoftwareInventory](/powershell/module/configurationmanager/Set-CMClientSettingSoftwareInventory)
- [Set-CMClientSettingSoftwareMetering](/powershell/module/configurationmanager/Set-CMClientSettingSoftwareMetering)
- [Set-CMClientSettingSoftwareUpdate](/powershell/module/configurationmanager/Set-CMClientSettingSoftwareUpdate)
- [Set-CMClientSettingStateMessaging](/powershell/module/configurationmanager/Set-CMClientSettingStateMessaging)
- [Set-CMClientSettingUserAndDeviceAffinity](/powershell/module/configurationmanager/Set-CMClientSettingUserAndDeviceAffinity)

Use the following cmdlets to manage deployments of custom client settings:

- [New-CMClientSettingDeployment](/powershell/module/configurationmanager/New-CMClientSettingDeployment)
- [Remove-CMClientSettingDeployment](/powershell/module/configurationmanager/Start-CMClientSettingDeployment)

## Next steps

[About client settings](about-client-settings.md)
