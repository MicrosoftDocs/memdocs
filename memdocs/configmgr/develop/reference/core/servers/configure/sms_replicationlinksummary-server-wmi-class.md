---
description: Learn how to use the SMS_ReplicationLinkSummary class to represent summaries of database replication link statuses.
title: SMS_ReplicationLinkSummary Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f5817089-7c5d-48bb-a0a7-415e7ccc4450
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ReplicationLinkSummary Server WMI Class
The `SMS_ReplicationLinkSummary` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the summary of database replication link status.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ReplicationLinkSummary : SMS_BaseClass  
{  
    String GlobalInitPercentage;  
    UInt32 LinkStatus;  
    UInt32 LinkStatusDescription;  
    String Site1;  
    UInt32 Site1Status;  
    UInt32 Site1ToSite2GlobalState;  
    DateTime Site1ToSite2GlobalSyncTime;  
    String Site2;  
    UInt32 Site2Status;  
    UInt32 Site2ToSite1GlobalState;  
    DateTime Site2ToSite1GlobalSyncTime;  
    UInt32 Site2ToSite1SiteState;  
    DateTime Site2ToSite1SiteSyncTime;  
    String SiteName1;  
    String SiteName2;  
    UInt32 SiteType1;  
    UInt32 SiteType2;  
};  
```  

## Methods  
 The `SMS_ReplicationLinkSummary` class does not define any methods.  

## Properties  
 `GlobalInitPercentage`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Progress of the re-initialization of the global data.  

 `LinkStatus`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Overall link status.  

 `LinkStatusDescription`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Overall link status.  

 `Site1`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Parent site for the link.  

 `Site1Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Site status for the parent site. See [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md).  

 `Site1ToSite2GlobalState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Overall link status for global data sent from the parent site to the child site.  

 `Site1ToSite2GlobalSyncTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last time that the parent site sent a message to the child site for global data synchronization.  

 `Site2`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Child site.  

 `Site2Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Site status for the child site. See [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md).  

 `Site2ToSite1GlobalState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Overall link status for global data sent from the child site to the parent site.  

 `Site2ToSite1GlobalSyncTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last time that the child site sent a message to the parent site for global data synchronization.  

 `Site2ToSite1SiteState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Overall link status for site data send from the child site to the parent site.  

 `Site2ToSite1SiteSyncTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last time that the child site sent a message to the parent site for data synchronization.  

 `SiteName1`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the parent site.  

 `SiteName2`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the child site.  

 `SiteType1`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Type of the parent site. Possible values are:  

|Value|Parent site type|  
|-|-|  
|1|SECONDARY|  
|2|PRIMARY|  
|4|CAS|  

 `SiteType2`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Type of the child site. Possible values are:  

|Value|Child site type|  
|-|-|  
|1|SECONDARY|  
|2|PRIMARY|  
|4|CAS|  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
