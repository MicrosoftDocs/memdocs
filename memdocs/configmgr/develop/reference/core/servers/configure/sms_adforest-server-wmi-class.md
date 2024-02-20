---
title: SMS_ADForest Class
titleSuffix: Configuration Manager
description: An SMS Provider server class that contains Active Directory forests discovered by Configuration Manager Forest Discovery.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 48fec821-d482-465c-b88e-d7f4852f1777
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ADForest Server WMI Class
The `SMS_ADForest` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that contains Active Directory forests discovered by Configuration Manager Forest Discovery.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ADForest : SMS_BaseClass  
{  
    String Account;  
    String CreatedBy;  
    DateTime CreatedOn;  
    String Description;  
    UInt32 DiscoveredADSites;  
    UInt32 DiscoveredDomains;  
    UInt32 DiscoveredIPSubnets;  
    UInt32 DiscoveredTrusts;  
    UInt32 DiscoveryStatus;  
    Boolean EnableDiscovery;  
    String ForestFQDN;  
    UInt32 ForestID;  
    String ModifiedBy;  
    DateTime ModifiedOn;  
    String PublishingPath;  
    UInt32 PublishingStatus;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_ADForest` class.  

|Method|Description|  
|------------|-----------------|  
|[DeleteDiscoveryData Method in Class SMS_ADForest](../../../../../develop/reference/core/servers/configure/deletediscoverydata-method-in-class-sms_adforest.md)|Removes information gathered by the forest discovery process.|  

## Properties  
 `Account`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Account to discover the Active Directory forest.  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User that added the Active Directory forest.  

 `CreatedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date the Active Directory forest was added.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the Active Directory forest.  

 `DiscoveredADSites`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of discovered Active Directory sites.  

 `DiscoveredDomains`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of discovered Active Directory domains.  

 `DiscoveredIPSubnets`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of discovered Active Directory IP subnets.  

 `DiscoveredTrusts`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Count of discovered Active Directory trusts.  

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

 `EnableDiscovery`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if Active Directory forest discovery is enabled.  

 `ForestFQDN`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 FQDN of the Active Directory forest.  

 `ForestID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifier of the Active Directory forest.  

 `ModifiedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User that last modified the Active Directory Forest.  

 `ModifiedOn`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date the Active Directory Forest was last modified.  

 `PublishingPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Alternate publishing path.  

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

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
