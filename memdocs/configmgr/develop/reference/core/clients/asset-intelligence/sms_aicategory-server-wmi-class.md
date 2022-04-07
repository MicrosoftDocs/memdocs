---
title: "SMS_AICategory Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager,the SMS_AICategory Windows Management Instrumentation class categorizes the software entries in the SMS_AISoftwareList Server WMI class." 
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9c90f84f-e111-4195-9063-a09eacd83c50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_AICategory Server WMI Class
The `SMS_AICategory` Windows Management Instrumentation (WMI) class, in Configuration Manager, categorizes the software entries in the `SMS_AISoftwareList` Server WMI class.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AICategory : SMS_BaseClass   
{   
      uint32 CategoryID;   
      string CategoryName;   
      string Description;   
      boolean IsLocal;   
      uint32 LanguageID;   
      uint32 State;   
      uint32 Type;   
};  
```  

## Methods  
 The following table lists the methods in the `SMS_AICategory` class.  

|Method|Description|  
|------------|-----------------|  
|[GetSummary Method in Class SMS_AICategory](../../../../../develop/reference/core/clients/asset-intelligence/getsummary-method-in-class-sms_aicategory.md)|Returns a summary of all defined categories.|  

## Properties  
 `CategoryID`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: key  

 Unique value for the record.  

 `CategoryName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Category display name.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Supplemental information that describes what this category is used for.  

 `IsLocal`  
 Data type: `Boolean`  

 Access type: Read Only  

 Qualifiers: None  

 `true` if this category instance was created locally. Categories that are created locally can be changed. When `false`, the `CategoryName` and `Description` properties are not editable.  

 `LanguageID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Language the category is written in.  

 `State`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: enumeration("STATE_VALIDATED(0), STATE_USER_DEFINED(1)")  

 Source of the category.  

|Value|Description|  
|-----------|-----------------|  
|0|Validated: Created by Microsoft.|  
|1|User Defined: Created by a user.|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Describes the way this category record is used.  

|Value|Description|  
|-----------|-----------------|  
|0|Category: Category this software fits into.<br />Example: Antivirus.|  
|1|Family: Family this software belongs in.<br />Example: Microsoft Office.|  
|2|Tag: User defined tags which are assigned to the software entries.<br />Example: Installed on a receptionist's computer.|  

## Remarks  
 Class qualifiers for this class include:  

- DisplayName("AI Category Table")  

- Dynamic  

- Provider("ExtnProv")  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
[Initiate Asset Intelligence synchronization](../../../../core/clients/asset-intelligence/how-to-initiate-a-synchronization.md)
