---
title: Device Management Server WMI Classes
titleSuffix: Configuration Manager
description: Device management server Windows Management Instrumentation (WMI) classes in Configuration Manager assist in assessment of computer compliance considering a number of mobile device configurations.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: cf75f787-c13e-49cf-9adb-e59cbb57bf7c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Device Management Server WMI Classes
Device management server Windows Management Instrumentation (WMI) classes in Configuration Manager assist in assessment of computer compliance considering a number of mobile device configurations.  

 The Configuration Manager server class schema is a set of WMI classes that represent the objects found on a server that is running Configuration Manager. Each Configuration Manager class is a template for a managed object and all instances of the object use the template. Classes can contain properties and methods. The properties describe the class data and the methods typically perform data management. For more information about developing applications using these classes, see [About Configuration Manager SDK Requirements](../../../develop/core/reqs/about-configuration-manager-sdk-requirements.md).  

## Mobile Device Management Classes  

-   [SMS_DeviceEnrollmentProfile Server WMI Class](../../../develop/reference/mdm/sms_deviceenrollmentprofile-server-wmi-class.md)  

-   [SMS_DeviceMethods Server WMI Class](../../../develop/reference/mdm/sms_devicemethods-server-wmi-class.md)  

-   [SMS_DeviceSettingItem Server WMI Class](../../../develop/reference/mdm/sms_devicesettingitem-server-wmi-class.md)  

-   [SMS_DeviceSettingPackage Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackage-server-wmi-class.md)  

-   [SMS_DeviceSettingPackageItem Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackageitem-server-wmi-class.md)  

## Remarks  
 Configuration Manager uses its device management functionality for mobile devices. It uses a special type of configuration item to represent a set of mobile device settings to apply to a mobile device. The device setting configuration item can only be distributed by using a device setting package that is accessible in the Configuration Package wizard in the Configuration Manager console. Source locations are defined automatically when creating the package.  

> [!NOTE]
>  Mobile devices do not have domain accounts and therefore do not recognize access account restrictions.  

## See Also  
 [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md)
