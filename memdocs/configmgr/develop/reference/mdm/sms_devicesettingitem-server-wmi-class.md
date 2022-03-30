---
title: "SMS_DeviceSettingItem Class"
titleSuffix: "Configuration Manager"
description: "The SMS_DeviceSettingItem WMI class provides the functionality to create a device setting configuration item in the database."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4381d1a1-ad59-4746-a8db-55d08e446dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_DeviceSettingItem Server WMI Class
The `SMS_DeviceSettingItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides the functionality to create a device setting configuration item in the database.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeviceSettingItem : SMS_BaseClass  
{  
    String Description;  
    String DeviceSettingItemUniqueID;  
    String Name;  
    String PropList;  
    String SourceSite;  
    String Type;  
    UInt32 Version;  
};  
```  

## Methods  
 The `SMS_DeviceSettingItem` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of the device setting to create. The default value is "".  

 `DeviceSettingItemUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 A GUID or unique ID that identifies the device setting item to create. The default value is "".  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique]  

 Name of the device setting item to create. The default value is "".  

 `PropList`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A list of properties for the device setting item.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The site code of the site for which to create the device setting item. The default value is "".  

 `Type`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Type of device setting item. The default value is "".  

 `Version`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the device setting item. The default value is 1.  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Device Management Server WMI Classes](../../../develop/reference/mdm/device-management-server-wmi-classes.md)
