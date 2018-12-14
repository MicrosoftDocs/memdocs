---
title: "SMS_SDMPackageLocalizedData Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c62cd280-81b8-46ee-9f92-0c063b1d2870
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_SDMPackageLocalizedData Server WMI Class
The `SMS_SDMPackageLocalizedData` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents localized data for a System Definition Model (SDM) package.  

## Syntax  

```  
Class SMS_SDMPackageLocalizedData  
{  
      UInt32 LocaleID;  
      String LocalizedData;  
};  
```  

## Methods  
 The `SMS_SDMPackageLocalizedData` class does not define any methods.  

## Properties  
 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The ID of the locale associated with the localized information.  

 `LocalizedData`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The localized data.  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is embedded by the [SMS_ConfigurationItemBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitembaseclass-server-wmi-class.md) through the `SDMPackageLocalizedData` property.  

  The application uses this class to add localized string resources to the server database.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_Package Server WMI Class](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
