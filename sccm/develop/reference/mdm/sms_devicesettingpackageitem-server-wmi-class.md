---
title: "SMS_DeviceSettingPackageItem Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 36769462-1a62-4830-8b44-bcd7386a508b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_DeviceSettingPackageItem Server WMI Class
The `SMS_DeviceSettingPackageItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that associates a device setting configuration item with a device setting package.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeviceSettingPackageItem : SMS_BaseClass  
{  
      String DeviceSettingItemUniqueID;  
      String PackageID;  
};  
```  

## Methods  
 The `SMS_DeviceSettingPackageItem` class does not define any methods.  

## Properties  
 `DeviceSettingItemUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 GUID or unique ID for the [SMS_DeviceSettingItem Server WMI Class](../../../develop/reference/mdm/sms_devicesettingitem-server-wmi-class.md) object that is contained in the [SMS_DeviceSettingPackage Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackage-server-wmi-class.md) object represented by `PackageID`. The default value is "".  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the [SMS_DeviceSettingPackage Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackage-server-wmi-class.md) object that contains the item represented by `DeviceSettingItemUniqueID`. The default value is "".  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Device Management Server WMI Classes](../../../develop/reference/mdm/device-management-server-wmi-classes.md)   
 [SMS_DeviceSettingItem Server WMI Class](../../../develop/reference/mdm/sms_devicesettingitem-server-wmi-class.md)   
 [SMS_DeviceSettingPackage Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackage-server-wmi-class.md)
