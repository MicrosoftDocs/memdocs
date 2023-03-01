---
description: Learn how to provide a summary report of the health of packages and distribution points in the site within Configuration Manager.
title: SMS_PackageStatus Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: d11a4300-8477-4d7b-a405-eb4e6f81e28e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_PackageStatus Server WMI Class
The `SMS_PackageStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides a summary report of the health of packages and distribution points in the site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_PackageStatus : SMS_BaseClass  
{  
      String Location;  
      String PackageID;  
      SInt32 Personality;  
      String PkgServer;  
      String ShareName;  
      String SiteCode;  
      SInt32 Status;  
      SInt32 Type;  
      DateTime UpdateTime;  
};  
```  

## Methods  
 The `SMS_PackageStatus` class does not define any methods.  

## Properties  
 `Location`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The Universal Naming Convention (UNC) path or network abstraction layer (NAL) path to where the package is stored or distributed.  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The unique local ID for the package.  

 `Personality`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration]  

 Status personality. Possible values are:  

|Value|Personality|  
|-|-|  
|0|NONE|  
|1|MAC|  
|2|FPNW|  

 `PkgServer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 If `Type` is MASTER (1), is the compressed copy of the package on the site server. If `Type` is COPY (2), `PkgServer` is the distribution point.  

 `ShareName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The share to which the package was distributed.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The site code for the site.  

 `Status`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration]  

 Status. Possible values are:  

|Value|Status|  
|-|-|  
|0|NONE|  
|1|SENT|  
|2|RECEIVED|  
|3|INSTALLED|  
|4|RETRY|  
|5|FAILED|  
|6|REMOVED|  
|7|PENDING_REMOVE|  

 `Type`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: [key, enumeration]  

 The status type. Possible values are:  

|Value|Status type|  
|-|-|  
|1|MASTER|  
|2|COPY|  

 `UpdateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: None  

 When `Type` is MASTER (1), the time when the compressed copy was created or merged. When `Type` is COPY (2), `UpdateTime` is the time when the distribution point was updated.  

## Remarks  
 Class qualifiers for this class include:  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

  This class is used internally by the server Distribution Manager component and is not used directly to produce any of the package status information that you see in the Configuration Manager console.  

  You can distribute multiple packages concurrently to multiple destinations. `SMS_PackageStatus` allows monitoring when packages arrive at distribution points. All the displayed dates are based on the time zone in which the Configuration Manager console is running.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)
