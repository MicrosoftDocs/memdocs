---
title: Capabilities in Technical Preview 1704
titleSuffix: Configuration Manager
description: Learn about features available in the Technical Preview for Configuration Manager, version 1704.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Capabilities in Technical Preview 1704 for Configuration Manager

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1704. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## Configure Android apps with app configuration policies
You can use app configuration policies in Configuration Manager to distribute settings that might be required when a user runs an app on Android for Work devices. Android app configuration policies are available only on devices running Android for Work and apply to approved apps from the Play for Work store.

### Try it out                 

In the Configuration Manager console, choose **Software Library** > **Application Management** > **App Configuration Policies** and choose **Create App Configuration Policy**. On the **General** page of the wizard, you can now **Select a configuration policy type**. Specify the platform targeted by the app configuration policy: **Configuration policy for Android for Work apps**. You can then either **Specify name and value pairs** or **Browse to a property list JSON file**. The new app configuration policy is shown in the **Software Library** workspace, in the **App Configuration Policies** node. To associate an app configuration policy with the deployment of an Android for Work app, deploy the application as you normally would by using the procedure in the [Deploy applications](../../apps/deploy-use/deploy-applications.md) topic.

## Hardware inventory collects Secure Boot information
Hardware inventory now collects information about whether Secure Boot is enabled on clients. This information is stored in the **SMS_Firmware** class (introduced in version 1702) and enabled in hardware inventory by default. For more information about hardware inventory, see  [How to configure hardware inventory](../clients/manage/inventory/configure-hardware-inventory.md).

## Add child task sequences to a task sequence
In this version, you can add a new task sequence step that runs another task sequence, which creates a parent/child relationship between the task sequences. This allows you to create more modular task sequences that you can re-use.  

Consider the following when you add a child task sequence to a task sequence:

- The parent and child task sequences are effectively combined into a single policy that the client runs.
- It is not supported to add a child task sequence that is a parent of another task sequence.
- The environment is global. For example, if a variable is set by the parent task sequence and then changed by the child task sequence, the variable remains changed moving forward. Similarly, if the child task sequence creates a new variable, the variable is available for the remaining steps in the parent task sequence.
- Status messages are sent per normal for a single task sequence operation.
- The task sequences write entries to the smsts.log file, with new log entries that make it clear when a child task sequence starts.
- In the Technical Preview for Configuration Manager, version 1704, if the child task sequences references any package and you run the parent task sequence from Software Center, the client will not find the package content when the child task sequence is run. In this scenario, you must run the task sequence from media (boot media, PXE, etc.).  

    If the child task sequence uses steps like **Run Command Line** (without any package reference), **Format**, **BitLocker**, etc., then the task sequence will run successfully from Software Center.

### To add a child task sequence to a task sequence
1. In the task sequence editor, click **Add**, select **General**, and click **Run Task Sequence**.
2. Click **Browse** to select the child task sequence.  

## Reload boot images with current Windows PE version
When you run **Update Distribution Points** on a selected boot image, you can now choose to reload the latest version of Windows PE (from the Windows ADK installation directory) in the boot image. The **General** page of the wizard provides information about the Windows ADK version installed on the site server, the Windows ADK version from which Windows PE was used in the boot image, and the version of the Configuration Manager client. You can use this information to help you decide whether to reload the boot image. Also, a new column (**Client Version**) has been added when you view boot images in the **Boot Images** node so you know what version of the Configuration Manager client each boot image uses.

### To reload a boot image with the current Windows PE version

1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Boot Images**.
2. Select a boot image and click **Update Distribution Points**.
3. On the **General** page of the wizard, select **Reload boot image using the current version of Windows PE from the installed Windows ADK**.

## Improvements to operating system deployment
We have made the following improvements to operating system deployment, which were the result of your feedback.

- New **OS Version** column for operating system images: We have added a new column named **OS Version** to display the version of the operating system for the image when you view information in the **Operating System Images** and **Operating System Upgrade Packages** nodes. Only the version of the first index in the .WIM is displayed. Go to the **Details** tab for the image to review operating system versions for other indexes.

- More efficient logging in Smsts.log: Beginning in this version, we are no longer writing entries to the smsts.log file for CCM_CIVersionInfo.PolicyID information. Prior to this version, there could be a lot of entries with this information, which made it hard to find more relevant information in the log file.
