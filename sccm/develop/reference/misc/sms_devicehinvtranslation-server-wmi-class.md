---
title: "SMS_DeviceHinvTranslation Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ca23c16e-0eab-42ef-b315-89cbf67f7d53
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_DeviceHinvTranslation Server WMI Class
The `SMS_DeviceHinvTranslation` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents a translation for an enumeration used in device hardware inventory.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_DeviceHinvTranslation : SMS_BaseClass  
{  
      String Item;  
      String Translation;  
};  
```  

## Methods  
 The `SMS_DeviceHinvTranslation` class does not define any methods.  

## Properties  
 `Item`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The enumeration, in the format Class:Property:Enumeration. An example is "Device_Computer_System:ProcessorArchitecture:5".  

 `Translation`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The enumeration value, for example, ARM.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The translations for the following enumerations are available in the product and additional translations might be added:  

-   Device_Computer_System:ProcessorArchitecture  

-   Device_Computer_System:ProcessorType  

-   Device_OS_INFORMATION:Platform  

-   Device_Power:AC  

-   Device_Power:Backup  

-   Device_Power:Battery  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Device Management Server WMI Classes](../../../develop/reference/mdm/device-management-server-wmi-classes.md)
