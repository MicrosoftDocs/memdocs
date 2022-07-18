---
title: Planning client deployment to Mac computers
titleSuffix: Configuration Manager
description: Plan for client deployment to Mac computers in Configuration Manager.
ms.date: 01/05/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---
# Planning for client deployment to Mac computers in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in January 2022, this feature of Configuration Manager is deprecated.<!-- 12927803 --> For more information, see [Mac computers](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).

You can install the Configuration Manager client on Mac computers that run macOS X and use the following management capabilities:  

- **Hardware inventory**  

   You can use Configuration Manager hardware inventory to collect information about the hardware and installed applications on Mac computers. This information can then be viewed in Resource Explorer in the Configuration Manager console and used to create collections, queries and reports. For more information, see [How to use Resource Explorer to view hardware inventory](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

   Configuration Manager collects the following hardware information from Mac computers:  

  -   Processor  

  -   Computer System  

  -   Disk Drive  

  -   Disk Partition  

  -   Network Adapter  

  -   Operating System  

  -   Service  

  -   Process  

  -   Installed Software  

  -   Computer System Product  

  -   USB Controller  

  -   USB Device  

  -   CDROM Drive  

  -   Video Controller  

  -   Desktop Monitor  

  -   Portable Battery  

  -   Physical Memory  

  -   Printer  

  > [!IMPORTANT]  
  >  You cannot extend the hardware information that is collected from Mac computers during hardware inventory.  

- **Compliance settings**  

   You can use Configuration Manager compliance settings to view the compliance of and remediate macOS X preference (.plist) settings. For example, you could enforce settings for the home page in the Safari web browser or ensure that the Apple firewall is enabled. You can also use shell scripts to monitor and remediate settings in macOS X.

- **Application management**  

   Configuration Manager can deploy software to Mac computers. You can deploy the following software formats to Mac computers:  

  - Apple disk image (.DMG)

  - Meta package file (.MPKG)

  - macOS X installer package (.PKG)

  - macOS X application (.APP)

  When you install the Configuration Manager client on Mac computers, you cannot use the following management capabilities that are supported by the Configuration Manager client on Windows-based computers:  

- Client push installation  

- Operating system deployment  

- Software updates  

  > [!NOTE]  
  >  You can use Configuration Manager application management to deploy required macOS X software updates to Mac computers. In addition, you can use compliance settings to make sure that computers have any required software updates.  

- Maintenance windows  

- Remote control  

- Power management  

- Client status client check and remediation  

  For more information about how to install and configure the Configuration Manager Mac client, see [How to deploy clients to Macs](../../../../core/clients/deploy/deploy-clients-to-macs.md).
