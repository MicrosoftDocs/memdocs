---
title: Download definitions from Microsoft
titleSuffix: Configuration Manager
description: Learn how to enable the download of Endpoint Protection malware definitions from Microsoft Updates for Configuration Manager.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Enable Endpoint Protection malware definitions to download from Microsoft Updates

*Applies to: Configuration Manager (current branch)*

When you select to download definition updates from Microsoft Update, clients will check the Microsoft Update site at the interval defined in the **Security Intelligence updates** section of the antimalware policy dialog box.

 This method can be useful when the client does not have connectivity to the Configuration Manager site or when you want users to be able to initiate definition updates.

> [!IMPORTANT]
> - Clients must have access to Microsoft Update on the Internet to be able to use this method to download definition updates.
> - The **Definition updates** section was renamed to **Security Intelligence updates** starting in Configuration Manager version 1902.

## Using the Microsoft Malware Protection Center to Download Definitions
 You can configure clients to download definition updates from the Microsoft Malware Protection Center. This option is used by Endpoint Protection clients to download definition updates if they have not been able to download updates from another source. This update method can be useful if there is a problem with your Configuration Manager infrastructure that prevents the delivery of updates.

> [!IMPORTANT]
>  Clients must have access to Microsoft Update on the Internet to be able use this method to download definition updates.
> 
> 
> [!div class="button"]
> [Next step >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Back >](endpoint-configure-alerts.md)
