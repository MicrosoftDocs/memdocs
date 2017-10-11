---
title: "SMS_ADSubnet Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: d07d5b73-8504-4ea1-9860-959f7dbd33ccsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ADSubnet Server WMI Class
The `SMS_ADSubnet` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains Active Directory subnets discovered by Configuration Manager Forest Discovery.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ADSubnet : SMS_BaseClass  
{  
    String ADSubnetDescription;  
    String ADSubnetLocation;  
    String ADSubnetName;  
    UInt32 Flags;  
    UInt32 ForestID;  
    DateTime LastDiscoveryTime;  
    UInt32 SiteID;  
    UInt32 SubnetID;  
};  
```  

## Methods  
 The `SMS_ADSubnet` class does not define any methods.  

## Properties  
 `ADSubnetDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Description of the Active Directory subnet.  

 `ADSubnetLocation`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Location of the Active Directory subnet.  

 `ADSubnetName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the Active Directory subnet.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Flags.   

 `ForestID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the Active Directory forest.  

 `LastDiscoveryTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 The last time this Active Directory subnet was discovered by Active Directory discovery.  

 `SiteID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Reference to the `SMS_ADSite SiteID` value.  

 `SubnetID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The subnet ID.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Discovery Server WMI Classes](../../../../../develop/reference/core/servers/configure/discovery-server-wmi-classes.md)
