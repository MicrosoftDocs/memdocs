---
title: "SMS_TaskSequencePackageReference_Flat Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7dba381c-b2b2-461b-8e7c-fd6aadd8739a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequencePackageReference_Flat Server WMI Class
The `SMS_TaskSequencePackageReference_Flat` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents all classic package or application references for a task sequence. The list also includes the applications that are dependent on the applications directly referenced in the task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequencePackageReference_Flat : SMS_BaseClass  
{  
    String Description;  
    String Level;  
    String ObjectID;  
    String ObjectName;  
    UInt32 ObjectType;  
    String PackageID;  
    String RefPackageID;  
    String SourceID;  
    UInt32 SourceSize;  
    String Version;  
};  
```  

## Methods  
 The `SMS_TaskSequencePackageReference_Flat` class does not define any methods.  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The description for the reference or dependent object.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 If the Task Sequence reference is to a legacy package, this property is the package identifier of the legacy package. If the Task Sequence reference is to an application, this property is the package identifier of the application.  

 `ObjectName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Display name for the reference or dependent object.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 The type of reference or dependent object. Possible values are:  

|||  
|-|-|  
|0|Classic Package|  
|3|Driver Package|  
|5|Software Update Package|  
|257|Operating System Image Package|  
|258|Boot Image Package|  
|259|Operating System Installer Source Package|  
|512|Application|  

 `Level`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: read  

 Reference or dependent object level in the dependency tree. For direct reference objects, this is 0.  

 `ObjectID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 If the Task Sequence reference is to a legacy package, this property is the package identifier of the legacy package. If the Task Sequence reference is to an application, this property is the package identifier of the application.  

 `ObjectName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Display name for the reference or dependent object.  

 `ObjectType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 The type of reference or dependent object. Possible values are:  

|||  
|-|-|  
|0|Classic Package|  
|3|Driver Package|  
|5|Software Update Package|  
|257|Operating System Image Package|  
|258|Boot Image Package|  
|259|Operating System Installer Source Package|  
|512|Application|  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Package identifier of the task sequence.  

 `RefPackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [none]  

 Reference or dependent object Package ID.  

 `SourceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [none]  

 Source object ID for dependency. For direct reference objects this s empty.  

 `SourceSize`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Package source size.  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [none]  

 Reference or dependent object version.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
