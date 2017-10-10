---
title: "SMS_MigrationSiteMapping Class"
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
ms.assetid: ac9084b4-13fd-4c95-a183-86508a2e1e07searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MigrationSiteMapping Server WMI Class
The `SMS_MigrationSiteMapping` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a mapping between the Configuration Manager source site and the System Center Configuration Manager top site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationSiteMapping : SMS_BaseClass  
{  
    String Account;  
    String AccountForSql;  
    String ContentDestination;  
    DateTime DateLastBegin;  
    DateTime DateLastSynced;  
    DateTime DateLastUpdated;  
    DateTime DateNextRun;  
    String DestinationSiteCode;  
    String DestinationSiteFQDN;  
    Boolean EnableDPSharing;  
    Boolean IsCentral;  
    Boolean IsDecommissioned;  
    Boolean IsDeleted;  
    UInt32 JobIDs[];  
    UInt32 MigratedClientNumber;  
    UInt32 MigratedObjectNumber;  
    String ModifiedBy;  
    String ParentSiteCode;  
    String ParentSiteServer;  
    String ScheduleToken;  
    UInt32 SiteMappingID;  
    String SourceSiteCode;  
    String SourceSiteFQDN;  
    UInt32 Status;  
    UInt32 SyncedEntities[];  
    UInt32 TotalClientNumber;  
    UInt32 TotalObjectNumber;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_MigrationSiteMapping` class.  

|Method|Description|  
|------------|-----------------|  
|[ActivateHierarchy Method in Class SMS_MigrationSiteMapping](../../../../develop/reference/core/migration/activatehierarchy-method-in-class-sms_migrationsitemapping.md)|Activates the hierarchy.|  
|[CleanupHierarchyData Method in Class SMS_MigrationSiteMapping](../../../../develop/reference/core/migration/cleanuphierarchydata-method-in-class-sms_migrationsitemapping.md)|Cleans up hierarchy data.|  
|[CheckDecommissionState Method in Class SMS_MigrationSiteMapping](../../../../develop/reference/core/migration/checkdecommissionstate-method-in-class-sms_migrationsitemapping.md)|Checks to see if site mapping can be decommissioned.|  
|[Decommission Method in Class SMS_MigrationSiteMapping](../../../../develop/reference/core/migration/decommission-method-in-class-sms_migrationsitemapping.md)|Decommissions site mapping.|  
|[Resuscitate Method in Class SMS_MigrationSiteMapping](../../../../develop/reference/core/migration/resuscitate-method-in-class-sms_migrationsitemapping.md)|Resuscitates site mapping.|  
|[Sync Method in Class SMS_MigrationSiteMapping](../../../../develop/reference/core/migration/sync-method-in-class-sms_migrationsitemapping.md)|Synchronizes the entities on the source site.|  

## Properties  
 `Account`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 SDK Account used for migration.  

 `AccountForSql`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 SQL Account used for migration.  

 `ContentDestination`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The destination of the content of the packages from this site..  

 `DateLastBegin`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last begin time.  

 `DateLastSynced`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last sync time.  

 `DateLastUpdated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Updated time.  

 `DateNextRun`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Next run time.  

 `DestinationSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Destination site code.  

 `DestinationSiteFQDN`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Destination site FQDN.  

 `EnableDPSharing`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if it should gather distribution point information.  

 `IsCentral`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the source site is a central site.  

 `IsDecommissioned`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the site has stopped gathering data.  

 `IsDeleted`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the site mapping has been deleted.  

 `JobIDs`  
 Data type: `UInt32 Array`  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 Jobs associated with this site mapping.  

 `MigratedClientNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Total number of migrated clients.  

 `MigratedObjectNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Total number of migrated objects.  

 `ModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Modified by.  

 `ParentSiteCode`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Parent site code for source site.  

 `ParentSiteServer`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Parent site server for source site.  

 `ScheduleToken`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Schedule token for the site mapping synchronization.  

 `SiteMappingID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Primary site mapping ID.  

 `SourceSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Source site code.  

 `SourceSiteFQDN`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Source site FQDN.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Site mapping synchronization status.  

|||  
|-|-|  
|0|Have not gathered data|  
|1|Ready for next data gathering process|  
|2|Gathering data|  
|3|Failed|  
|4|Stopped|  
|258|Gathering hierarchy data|  
|259|Failed (Unauthorized Access)|  
|514|Gathering object data|  
|515|Failed (Network Timeout)|  
|770|Gathering client data|  
|771|Failed (No Permission to Source Site WMI)|  
|1026|Gathering package status data|  
|1027|Failed (SQL Error)|  
|1283|Failed (Child Primary Site)|  
|1539|Failed (Same Hierarchy)|  
|1795|Failed (Unsupported Site Version)|  
|2051|Failed (No Permission to fnSCCMMultiByteToWideChar)|  
|2307|Failed (Duplicated site code with current hierarchy)|  
|4099|Failed (Duplicated site code with another source hierarchy)|  

 `SyncedEntities`  
 Data type: `UInt32 Array`  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 Entities synchronized from this site mapping.  

 `TotalClientNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Total number of clients.  

 `TotalObjectNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Total number of objects.  

## Remarks  
 Once a source site is configured for data gathering, it should appear as an instance of this class. This instance controls many aspects of the data gathering, such as the schedule, whether distribution point sharing is enabled, and so on. It also has some monitoring data such as status, the total object number and the total client number.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
