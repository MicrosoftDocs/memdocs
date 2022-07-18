---
title: "SMS_WindowsServicingLocalizedNames Class"
titleSuffix: "Configuration Manager"
description: "The SMS_WindowsServicingLocalizedNames Server WMI Class is for internal use only.For more information about both the class qualifiers and the property qualifiers, see Configuration Manager Class and Property Qualifiers."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8006315c-6687-439d-b3a8-f013af7d7be4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_WindowsServicingLocalizedNames Server WMI Class
For internal use only.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_WindowsServicingLocalizedNames : SMS_BaseClass  
{  
    UInt32 LocaleID;  
    String Name;  
    String Value;  
};  

```  

## Methods  
 The  `SMS_WindowsServicingLocalizedNames` class does not define any methods.  

## Properties  
 `LocaleID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Reserved for internal use.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Reserved for internal use.  

 `Value`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Reserved for internal use.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
