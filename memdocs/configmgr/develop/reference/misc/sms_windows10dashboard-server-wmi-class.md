---
title: "SMS_Windows10Dashboard Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d5234925-8951-45ab-89d4-e5b9f582e800
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Windows10Dashboard Server WMI Class
For internal use only.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Windows10Dashboard : SMS_BaseClass  
{  
    String Branch;  
    String Build;  
    String Name;  
    UInt32 NumClients;  
    UInt32 State;  
};  

```  

## Methods  
 The `SMS_Windows10Dashboard` class does not define any methods.  

## Properties  
 `Branch`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Reserved for internal use.  

 `Build`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 Reserved for internal use.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Reserved for internal use.  

 `NumClients`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Reserved for internal use.  

 `State`  
 Data type: `UInt32`  

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
