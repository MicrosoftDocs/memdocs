---
description: Learn how to use the SMS_CI_LocalizedProperties class in Configuration Manager which contains the localized properties for a configuration item.
title: "SMS_CI_LocalizedProperties Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b74eec73-00a3-40ad-a496-fa42d80f0c27
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CI_LocalizedProperties Server WMI Class
The `SMS_CI_LocalizedProperties` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains the localized properties for a configuration item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CI_LocalizedProperties  
{  
      String Description;  
      String DisplayName;  
      String InformativeURL;  
      UInt32 LocaleID;  
};  
```  

## Methods  
 The `SMS_CI_LocalizedProperties` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of the configuration item. The default value is "".  

 `DisplayName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Display name for the configuration item. The default value is "".  

 `InformativeURL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 URL identifying additional information about the configuration item. The default value is "".  

 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the locale associated with the localized properties for the configuration item.  

## Remarks  
 Class qualifiers for this class include:  

- Embedded  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is embedded by the following classes, through the `LocalizedInformation` property:  

- [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)  

- [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)  

- [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)  

- [SMS_AuthorizationList Server WMI Class](../../../develop/reference/sum/sms_authorizationlist-server-wmi-class.md)  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)   
 [SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)   
 [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)   
 [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)   
 [SMS_AuthorizationList Server WMI Class](../../../develop/reference/sum/sms_authorizationlist-server-wmi-class.md)
