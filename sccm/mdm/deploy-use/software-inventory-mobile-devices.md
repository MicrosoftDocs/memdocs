---
title: "Software Inventory for Mobile Devices Enrolled with Microsoft Intune"
titleSuffix: "Configuration Manager"
description: "Software inventory for mobile devices enrolled with Microsoft Intune."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
---
# Software inventory for mobile devices enrolled with Microsoft Intune

*Applies to: System Center Configuration Manager (Current Branch)*

 You can collect inventory for apps installed on mobile devices. The apps that are inventoried will depend on whether the device is company-owned or personal-owned. For personal devices, the only apps that are inventoried are apps that are managed by Microsoft Intune.  

> [!NOTE]  
>  Inventory on the apps installed on mobile devices is collected as part of the [hardware inventory](mobile-device-hardware-inventory-hybrid.md) process.  

 Here are the apps that are inventoried for personal-owned or company-owned devices.  

|Platform|For Personal-owned Devices|For Company-owned devices|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (without the Configuration Manager client)|Only managed apps|Only managed apps|
|Windows 8.1 (without the Configuration Manager client)|Only managed apps|Only managed apps|  
|Windows Phone 8|Only managed apps|Only managed apps|  
|Windows RT|Only managed apps|Only managed apps|  
|iOS|Only managed apps|All apps installed on the device|  
|Android|Only managed apps|All apps installed on the device|  

See [Introduction to software inventory](../../core/clients/manage/inventory/introduction-to-software-inventory.md) and [How to configure software inventory ](../../core/clients/manage/inventory/configure-software-inventory.md) for detailed information about using software inventory to collect file information on client devices.
