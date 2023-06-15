---
title: SMS_CM_UpdatePackageSiteStatus Class
titleSuffix: Configuration Manager
description: The  `SMS_CM_UpdatePackageSiteStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is used to get the update package installation status per site.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8183768c-9786-4dfa-9bc4-f3198a9dd594
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CM_UpdatePackageSiteStatus Server WMI Class
The  `SMS_CM_UpdatePackageSiteStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is used to get the update package installation status per site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_UpdatePackageSiteStatus : SMS_BaseClass  
{  
    DateTime LastUpdateTime;    
    String Name;  
    String PackageGuid;  
    SInt32 PrereqFlag;  
    String SiteCode;  
    String SiteName;  
    SInt32 SiteNumber;  
    String SiteServerName;  
    Sint32 SiteType;  
    Sint32 State;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_CM_UpdatePackageSiteStatus` class.  

|Method|Description|  
|------------|-----------------|  
|[UpdatePackageSiteState Method in Class SMS_CM_UpdatePackageSiteStatus](../../../develop/reference/sum/updatepackagesitestate-method-in-class-sms_cm_updatepackagesitestatus.md)|Updates the package installation state of the site.|  

## Properties  
 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: none  

 The date and time that the state was last updated.  

 `Name`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the update package.  

 `PackageGuid`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 The unique identifier of the package.  

 `PrereqFlag`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Prerequisite flag. Possible values are: bits:  

| Value | Description |  
| ----- | ----------- |  
|0x1|Prereq only|  
|0x2|CONTINUE_ON_PREREQ_WARNING|  

 `SiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The site code.  

 `SiteName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The name of the site.  

 `SiteNumber`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read, key, not_null]  

 The unique identifier of the site.  

 `SiteServerName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The site server name.  

 `SiteType`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 The site type.  

 `State`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The state of the installation.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
