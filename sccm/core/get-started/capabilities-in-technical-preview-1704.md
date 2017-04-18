---
title: "Capabilities in Technical Preview 1704 Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1704."
ms.custom: na
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1704 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1704. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## Hardware inventory collects Secure Boot information
Hardware inventory now collects information about whether Secure Boot is enabled on clients. This information is stored in the **SMS_Firmware** class (introduced in version 1702) and enabled in hardware inventory by default. For more information about hardware inventory, see  [How to configure hardware inventory](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

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
When you run **Update Distribution Points** on a selected boot image, you can now choose to reload the latest version of Windows PE (from the Windows ADK installation directory) in the boot image. The **General** page of the wizard provides information about the Windows ADK version installed on the site server and the Windows ADK version from which Windows PE was used in the boot image. You can use this information to help you decide whether to reload Windows PE in the boot image with the current version.  

### To reload a boot image with the current Windows PE version

1. In the Configuration Manager console, go to **Software Library** > **Operating Systems** > **Boot Images**.
2. Select a boot image and click **Update Distribution Points**.
3. On the **General** page of the wizard, select **Reload boot image using the current version of Windows PE from the installed Windows ADK.
