---
title: "SMS_CIUpdateSources Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 475fd0a6-dd50-4b4c-8b84-ebe32129d40f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_CIUpdateSources Server WMI Class
The `SMS_CIUpdateSources` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides information on all the update sources associated with an [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md) object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CIUpdateSources : SMS_BaseClass  
{  
    UInt32 CI_ID;  
    DateTime DateCreated;  
    DateTime DateModified;  
    UInt32 MinSourceVersion;  
    String ModelName;  
    UInt32 UpdateSource_ID;  
};  
```  

## Methods  
 The `SMS_CIUpdateSources` class does not define any methods.  

## Properties  
 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the configuration item corresponding to the software update. This ID is unique only for the site. The ID is defined by the `CI_ID` property of SMS_ConfigurationItemBaseClass Server WMI Class.  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 Date and time when the configuration was created.  

 `DateModified`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 The last date and time when the configuration item was modified.  

 `MinSourceVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Minimum version of the source in which the update was found.  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `UpdateSource_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID of the software update source. Supported sources are Windows Server Update Services (WSUS) and ITMU/Offline Catalog. For more information, see [SMS_SoftwareUpdateSource Server WMI Class](../../../develop/reference/sum/sms_softwareupdatesource-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class in synchronizing software update metadata so that correct information can be obtained from a source during software update deployment.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_SoftwareUpdate Server WMI Class](../../../develop/reference/sum/sms_softwareupdate-server-wmi-class.md)   
 [SMS_SoftwareUpdateSource Server WMI Class](../../../develop/reference/sum/sms_softwareupdatesource-server-wmi-class.md)   
 [About software update deployments](../../sum/about-software-updates-deployments.md)
