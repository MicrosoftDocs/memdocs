---
title: "SMS_PkgToPkgProgram_a Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: ce226b54-3289-48fb-937a-f2730cca6d4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_PkgToPkgProgram_a Server WMI Class
The `SMS_PkgToPkgProgram_a` association Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that uses the `PackageID` property to relate an [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object with related [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md) objects.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PkgToPkgProgram_a : SMS_BaseAssociation  
{  
     ref:SMS_Package package;  
     ref:SMS_Program pkgProgram;  
};  
```  

## Methods  
 The `SMS_PkgToPkgProgram_a` class does not define any methods.  

## Properties  
 `package`  
 Data type: `ref:SMS_Package`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) object path.  

 `pkgProgram`  
 Data type: `ref:SMS_Program`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to an [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md) object path.  

## Remarks  
 Class qualifiers for this class include:  

- Association: ToInstance  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Software Distribution Server WMI Classes](../../../../../develop/reference/core/servers/configure/software-distribution-server-wmi-classes.md)   
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [SMS_Program Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md)
