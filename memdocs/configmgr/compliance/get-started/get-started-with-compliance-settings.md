---
title: Get started with compliance settings
titleSuffix: Configuration Manager
description: Learn about core concepts and how compliance settings work
ms.date: 01/04/2022
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Get started with compliance settings in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Before creating Configuration Manager compliance settings, first learn about core concepts and understand how they work.  

## How compliance settings work

Compliance settings let you manage the configuration and compliance of clients in your organization.  

Configuration items fall into two main categories:  

- **Settings for devices that are managed with the Configuration Manager client** - typically devices on which you've installed Configuration Manager client software to let you manage the device.  

- **Settings for devices that are managed without the Configuration Manager client** - typically devices that are managed with Microsoft Intune, or with Configuration Manager on-premises device management.  

## What devices are supported?  

| Device type | More information |  
|------------|----------------------|  
| Windows PCs (with the Configuration Manager client) | Create custom configuration items to assess objects such as registry keys, files, and Active Directory attributes.<br /><br /> When you use the Windows 10 or later configuration item type, select settings from a predefined list. |  
| Windows PCs (enrolled with on-premises MDM) | Select settings from a predefined list. |  
| Windows Phone devices (enrolled with on-premises MDM) | Select settings from a predefined list. |  
| Mac computers (with the Configuration Manager client) | Create custom configuration items to assess objects such as macOS preferences, and results returned by a script. |  

> [!NOTE]
> On-premises MDM and the Configuration Manager client for macOS are both deprecated. For more information, see [Removed and deprecated features for Configuration Manager](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 12454901,12927803 -->

## What is a configuration item?

A configuration item is a container that stores specific information. The information you configure depends on the configuration item type. Configuration items can include the following information:

- **Detection method information** is only for Windows configuration items that contain application settings. It detects whether an application is installed. This detection uses the Windows installer file for the application, or by using a custom script.  

- **Settings** represent the business or technical conditions to assess compliance on client devices. Configure a new setting or browse to an existing setting on a reference computer.  

- **Compliance rules** specify the conditions that define the compliance of a configuration item setting. Before the client evaluates a setting for compliance, it must have at least one compliance rule. Some settings remediate noncompliant values. Create new rules, or browse to an existing setting in any configuration item and select rules in it.  

- **Supported platforms** are the device platforms you define on which the client evaluates compliance of the configuration items. If you deploy a configuration item to a device that is not in the supported platforms list, it does not evaluate compliance.  

## What is a configuration baseline?

Define a configuration baseline that includes the configuration items to evaluate. Also include the settings and rules that describe the required level of compliance. Import this configuration data from Configuration Manager configuration packs. Microsoft and other vendors define these configuration packs. Or create new configuration items and configuration baselines.  

After you define a configuration baseline, deploy it to user and device collections. The client then evaluates the baseline settings for compliance on a schedule. You can deploy more than one configuration baseline to devices. This granularity provides greater control of compliance. 

Client devices evaluate their compliance against each deployed configuration baseline and immediately report the results to the site by using state messages and status messages. If a device is currently disconnected from the network, but downloaded the configuration baseline, it still evaluates compliance of the configuration items. It sends the compliance information when it reconnects.  

### Monitoring configuration baselines

- Monitor the results of the compliance evaluation in the Configuration Manager console, under the **Monitoring** workspace, in the **Deployments** node. For example:
  - Common causes of noncompliance
  - Errors
  - The number of affected users and devices
- Run compliance settings reports with additional details. For example:
  - Which devices are compliant or non-compliant
  - Which element of the configuration baseline is causing a computer to be non-compliant
- View compliance evaluation results from Windows computers running the Configuration Manager client. Open the **Configuration Manager** control panel, and switch to the **Configurations** tab.  

## User data and profiles configuration items

Configuration items for user data and profiles include settings that control how users on computers that run Windows 8 and later manage:  

- Folder redirection
- Offline files
- Roaming profiles  

Deploy these configuration items to user collections. Monitor their compliance from the **Monitoring** node of the Configuration Manager console. Unlike other configuration items, don't add them to configuration baselines before you deploy them. Deploy them directly by clicking **Deploy** in the ribbon.  

For more information, see [Create user data and profiles configuration items](../deploy-use/create-user-data-and-profiles-configuration-items.md).  

## Remote connection profiles  

Remote connection profiles provide a set of tools and resources to help you create, deploy, and monitor remote connection settings. By deploying these settings to devices, you minimize the effort that end users require to connect their computers to the corporate network.  

For more information, see [Create remote connection profiles](../deploy-use/create-remote-connection-profiles.md).  

## Windows edition upgrade

The edition upgrade policy automatically upgrades devices that run certain versions of Windows 10 to a newer edition. This policy supplies a new product key or license file that the device consumes to upgrade.

For more information, see [Upgrade Windows devices with the edition upgrade policy](../deploy-use/upgrade-windows-version.md)

## Next steps

[Plan for and configure compliance settings](../plan-design/plan-for-and-configure-compliance-settings.md)
