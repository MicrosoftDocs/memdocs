---
description: Article detailing the use of SMS_ClientDeploymentStateDetailsView in Configuration Manager.
title: "SMS_ClientDeploymentStateDetailsView Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 6f8ad726-3bb7-4d01-98b9-f3b08459edef
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ClientDeploymentStateDetailsView Server WMI Class
The `SMS_ClientDeploymentStateDetailsView` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a client deployment state details view.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ClientDeploymentStateDetailsView: SMS_BaseClass  
{  
    UInt32 BaselineItemID;  
    String BaselineItemName;  
    UInt32 BaselineItemType;  
    String NetBiosName;      
    UInt32 RecordID;  
    String SMSID;  
};  

```  

## Methods  
 The  `SMS_ClientDeploymentStateDetailsView` class does not define any methods.  

## Properties  
 `BaselineItemID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The client baseline item ID.  

 `BaselineItemName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The client baseline item name.  

 `BaselineItemType`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 The client baseline item type. Possible values are:  

|Value|Baseline item type|  
|-|-|  
|1|Patch or CU|  
|2|Language Pack|  

 `NetBiosName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The NetBIOS name of the client.  

 `RecordID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The record ID of the client deployment state.  

 `SMSID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The SMSID of the client.  

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
