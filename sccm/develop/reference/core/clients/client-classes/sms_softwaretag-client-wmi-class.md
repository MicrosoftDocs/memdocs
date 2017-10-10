---
title: "SMS_SoftwareTag Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 480a698f-3120-4469-9a9b-aa7a83fce474searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SoftwareTag Client WMI Class
The `SMS_SoftwareTag` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that indicates the presence of a software application on a computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SoftwareTag  
{  
      String DisplayVersion;  
      Boolean EntitlementRequired;  
      String ProductName;  
      String SoftwareCreator;  
      String SoftwareCreatorRegid;  
      String SoftwareLicensor;  
      String SoftwareLicensorRegid;  
      String TagCreator;  
      String TagCreatorRegid;  
      String UniqueID;  
      SInt32 VersionMajor;  
      SInt32 VersionMinor;  
};  
```  

## Methods  
 The `SMS_SoftwareTag` class does not define any methods.  

## Properties  
 `DisplayVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Display version.  

 `EntitlementRequired`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: None  

 `true` if the software application requires a license entitlement grant from the software publisher prior to usage.  

 `ProductName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Product name used as a display name used in reports.  

 `SoftwareCreator`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Software creator.  

 `SoftwareCreatorRegid`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Registration identifier of the software creator.  

 `SoftwareLicensor`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Software licensor.  

 `SoftwareLicensorRegid`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: None  

 Registration identifier of the software licensor.  

 `TagCreator`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Tag creator.  

 `TagCreatorRegid`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: key  

 Registration identifier of the tag creator.  

 `UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: key  

 Unique identier.  

 `VersionMajor`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Major version of the software.  

 `VersionMinor`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: None  

 Minor version of the software.  

## Remarks  

> [!NOTE]
>  This class is not currently used to support existing Asset Intelligence reports. However, it can be enabled to support custom reports.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Asset Intelligence Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/asset-intelligence-client-wmi-classes.md)   
 [SMS_AutoStartSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_autostartsoftware-client-wmi-class.md)   
 [SMS_BrowserHelperObject Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_browserhelperobject-client-wmi-class.md)   
 [SMS_InstalledExecutable Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedexecutable-client-wmi-class.md)   
 [SMS_InstalledSoftware Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftware-client-wmi-class.md)   
 [SMS_InstalledSoftwareMS Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_installedsoftwarems-client-wmi-class.md)   
 [SMS_Processor Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_processor-client-wmi-class.md)   
 [SMS_SystemConsoleUsage Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleusage-client-wmi-class.md)   
 [SMS_SystemConsoleUser Client WMI Class](../../../../../develop/reference/core/clients/client-classes/sms_systemconsoleuser-client-wmi-class.md)
