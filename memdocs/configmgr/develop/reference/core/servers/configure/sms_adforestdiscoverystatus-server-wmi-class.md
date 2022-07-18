---
description: Learn how to represent the status of Configuration Manager Active Directory Forest Discovery with SMS_ADForestDiscoveryStatus.
title: "SMS_ADForestDiscoveryStatus Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: ef766ce5-3137-43b7-8029-26e0606391d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ADForestDiscoveryStatus Server WMI Class
The `SMS_ADForestDiscoveryStatus` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the status of Configuration Manager Active Directory Forest Discovery.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ADForestDiscoveryStatus : SMS_BaseClass  
{  
    Boolean DiscoveryEnabled;  
    UInt32 DiscoveryStatus;  
    UInt32 ForestID;  
    DateTime LastDiscoveryTime;  
    DateTime LastPublishingTime;  
    Boolean PublishingEnabled;  
    UInt32 PublishingStatus;  
    String SiteCode;  
    String SiteName;  
};  
```  

## Methods  
 The `SMS_ADForestDiscoveryStatus` class does not define any methods.  

## Properties  
 `DiscoveryEnabled`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if forest discovery is enabled.  

 `DiscoveryStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Discovery status. Possible values are:  

|Value|Discovery status|  
|-|-|  
|0|SUCCEEDED|  
|1|COMPLETED|  
|2|ACCESS_DENIED|  
|3|FAILED|  
|4|STOPPED|  

 `ForestID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the Active Directory forest.  

 `LastDiscoveryTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last time the forest was discovered.  

 `LastPublishingTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last time the forest was published.  

 `PublishingEnabled`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if Active Directory publishing is enabled.  

 `PublishingStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Publishing status. Possible values are:  

|Value|Publishing status|  
|-|-|  
|0|UNKNOWN|  
|1|SUCCEEDED|  
|2|FAILED|  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The site code where the Active Directory forest was discovered.  

 `SiteName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 The site name where the Active Directory forest was discovered.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
