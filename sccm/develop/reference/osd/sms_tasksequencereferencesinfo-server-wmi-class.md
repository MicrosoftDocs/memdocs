---
title: "SMS_TaskSequenceReferencesInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7ce8cfe5-c40f-447c-b5c5-e65ee25b3baf
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequenceReferencesInfo Server WMI Class
The `SMS_TaskSequenceReferencesInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that associates a task sequence with its package.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequenceReferencesInfo : SMS_BaseClass  
{  
      String PackageID;  
      String ProgramName;  
      String ReferenceDescription;  
      String ReferenceName;  
      String ReferencePackageID;  
      UInt32 ReferencePackageType;  
      String ReferenceProgramName;  
      String ReferenceVersion;  
};  
```  

## Methods  
 The `SMS_TaskSequenceReferencesInfo` class does not define any methods.  

## Properties  
 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 ID of the task sequence package.  

 `ProgramName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Name of the program associated with the task sequence.  

 `ReferenceDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The long description of the reference package.  

 `ReferenceName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The name of the reference package.  

 `ReferencePackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 ID of the reference package.  

 `ReferencePackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The type of the reference package. Possible values are:  

|||  
|-|-|  
|0 (0x0000)|PKG_TYPE_REGULAR|  
|3 (0x0003)|PKG_TYPE_DRIVER|  
|4 (0x0004)|PKG_TYPE_TASK_SEQUENCE|  
|5 (0x0005)|PKG_TYPE_SWUPDATES|  
|257 (0x0101)|PKG_TYPE_IMAGE|  
|258 0x0102)|PKG_TYPE_BOOTIMAGE|  
|259 (0x0101)|PKG_TYPE_OSINSTALLIMAGE|  

 `ReferenceProgramName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the reference program for the task sequence.  

 `ReferenceVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The version of the reference package.  

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
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
