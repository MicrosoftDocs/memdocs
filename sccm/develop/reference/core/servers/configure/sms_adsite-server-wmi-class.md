---
title: "SMS_ADSite Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 3f3335ad-f784-4bbc-bb98-a55726e07804
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_ADSite Server WMI Class
The `SMS_ADSite` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains Active Directory sites discovered by Configuration Manager Forest Discovery.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ADSite : SMS_BaseClass  
{  
    String ADSiteDescription;  
    String ADSiteLocation;  
    String ADSiteName;  
    UInt32 Flags;  
    UInt32 ForestID;  
    DateTime LastDiscoveryTime;  
    UInt32 SiteID;  
};  
```  

## Methods  
 The `SMS_ADSite` class does not define any methods.  

## Properties  
 `ADSiteDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the Active Directory site.  

 `ADSiteLocation`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Location of the Active Directory site.  

 `ADSiteName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the Active Directory site.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Flags.   

 `ForestID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The identifier of Active Directory forest.  

 `LastDiscoveryTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last time this Active Directory site was discovered by Active Directory forest discovery.  

 `SiteID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 SiteID …   

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Discovery Server WMI Classes](../../../../../develop/reference/core/servers/configure/discovery-server-wmi-classes.md)
