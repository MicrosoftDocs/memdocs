---
title: "SMS_UpdatePrograms Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: c4d9d58e-f897-4d7d-8fbe-bade03392abdsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_UpdatePrograms Server WMI Class
The `SMS_UpdatePrograms` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides information about programs used for a software update.  

> [!NOTE]
>  This class is included for backward compatibility only. It is not applicable to the current Configuration Manager version.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UpdatePrograms : SMS_BaseClass  
{  
      String PackageID;  
      UInt32 PackageType;  
      UInt32 PackageVersion;  
      String ProgramName;  
      UInt32 UpdateID;  
};  
```  

## Methods  
 The `SMS_UpdatePrograms` class does not define any methods.  

## Properties  
 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID of the package associated with the software update.  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The type of package, as defined by the `PackageType` property of the [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md). The default value is 0.  

 `PackageVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The version of the package. The default value is 0.  

 `ProgramName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The name of the program to use for the software update, for example, "Notepad.exe". The default value is "".  

 `UpdateID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The ID for the software update.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)   
 [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md)   
 [Configuration Manager Software Updates](../../../develop/sum/software-updates.md)
