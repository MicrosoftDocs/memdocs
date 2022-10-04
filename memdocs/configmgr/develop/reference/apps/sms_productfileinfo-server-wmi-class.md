---
title: SMS_ProductFileInfo Class
titleSuffix: Configuration Manager
description: The SMS_ProductFileInfo WMI class represents a combination of file and product information for inventory and metering.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ef754afa-1157-4213-8db5-b855c0bde8a5
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ProductFileInfo Server WMI Class
The `SMS_ProductFileInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a combination of file and product information for inventory and metering.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ProductFileInfo : SMS_BaseClass  
{  
      String CompanyName;  
      String FileDescription;  
      SInt64 FileID;  
      String FileName;  
      UInt32 FileSize;  
      String FileVersion;  
      UInt32 ProductLanguage;  
      String ProductName;  
      String ProductVersion;  
};  
```  

## Methods  
 The `SMS_ProductFileInfo` class does not define any methods.  

## Properties  
 `CompanyName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the company that made the file, taken from the `Company` property of the file version resources.  

 `FileDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of the file, taken from the file version resources.  

 `FileID`  
 Data type: `SInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Auto-incremented key.  

 `FileName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Name of the file.  

 `FileSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Size of the file.  

 `FileVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 File version of the file, taken from the file version resources.  

 `ProductLanguage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Language of the product.  

 `ProductName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Product name.  

 `ProductVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Product version, taken from the file version resources.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 This class provides the source for the `FileID` foreign key property in other classes. When a file is metered, information about the file is sent with the process execution information. This is a subset of the information that is reported by software inventory. The common information that is shared between software inventory and software metering is represented by this class, which lists every file known to the operating system.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
