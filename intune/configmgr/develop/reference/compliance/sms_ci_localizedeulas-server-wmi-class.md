---
title: SMS_CI_LocalizedEulas Class
titleSuffix: Configuration Manager
description: An SMS Provider server class in Configuration Manager. It contains the localized Microsoft Software License Terms information for a configuration item.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5e8ec642-51dc-4388-bbac-3a067addaed1
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CI_LocalizedEulas Server WMI Class
The `SMS_CI_LocalizedEulas` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains the localized Microsoft Software License Terms information for a configuration item.  

## Syntax  

```  
Class SMS_CI_LocalizedEulas  
{  
      String EULAContentUniqueID;  
      UInt32 LocaleID;  
};  
```  

## Methods  
 The `SMS_CI_LocalizedEulas` class does not define any methods.  

## Properties  
 `EULAContentUniqueID`  
 Data type: `String`  

 Access type: `Read/Write`  

 Qualifiers: `None`  

 Unique ID of the Microsoft Software License Terms content.  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: `Read/Write`  

 Qualifiers: `None`  

 The ID of the locale associated with the localized information.  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is embedded by the following classes, through the `LocalizedEulas` property:  

- [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)  

- [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)  

- [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)  

  Your application uses this class only if the `EULAExists` property of the configuration item is set to `true`.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)
