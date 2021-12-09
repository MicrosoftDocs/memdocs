---
title: "SMS_ClientBaselineItem Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 20ab5c14-ea0f-4490-99d8-0b1887705940
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientBaselineItem Server WMI Class
The `SMS_ClientBaselineItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a client deployment baseline item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientBaselineItem: SMS_BaseClass  
{  
    UInt32 BaselineFlags;  
    UInt32 BaselineItemID;  
    String Name;      
    UInt32 Platform;  
    UInt32 Type;  
    String UniqueID;  
};  

```  

## Methods  
 The `SMS_ClientBaselineItem` class does not define any methods.  

## Properties  
 `BaselineFlags`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Baseline flags to indicate which baseline this item belongs to.  

 `BaselineItemID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 Client baseline item ID.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Client baseline item name.  

 `Platform`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 The platform of the client baseline item. Possible values are:  

|Value|Platform|  
|-|-|  
|1|x86|  
|2|x64|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 The client baseline item type. Possible values are:  

|Value|Baseline item type|  
|-|-|  
|1|Patch or CU|  
|2|Language Pack|  

 `UniqueID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The GUID of the client baseline item.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
