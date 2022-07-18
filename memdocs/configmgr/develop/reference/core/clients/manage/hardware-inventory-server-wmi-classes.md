---
title: Hardware inventory server WMI classes
titleSuffix: Configuration Manager
description: "The Configuration Manager hardware inventory server WMI classes are generated dynamically and the name for a class is transformed from Win32_hardware to SMS_G_System_hardware."
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2cc63027-0dbd-4842-933d-171ee66d7c0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---

# Hardware inventory server WMI classes

The Configuration Manager hardware inventory server WMI classes are generated dynamically.  

During the Configuration Manager hardware inventory process, the name for a class is transformed from "Win32_hardware" to "SMS_G_System_hardware". For example, "Win32_DiskDrive" translates to "SMS_G_System_DISK".  

In addition to the class name change, the following differences are found between the Win32 classes and the Configuration Manager hardware inventory server classes:  

- Each Configuration Manager class inherits four properties from [SMS_G_System_Current Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_g_system_current-server-wmi-class.md).  

- The Configuration Manager hardware inventory classes don't support the Win32 class methods.  

- Many of the Configuration Manager hardware inventory classes contain a subset of the Win32 class properties.  

