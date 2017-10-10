---
title: "SMS_MigrationJob Class"
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
ms.assetid: 6ecbb0a8-2ed4-40d0-ba75-5d0c7c484b58searchScope: - ConfigMgr SDK
caps.latest.revision: 17
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MigrationJob Server WMI Class
The `SMS_MigrationJob` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a migration job.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationJob : SMS_BaseClass  
{  
    String AdditionalConfiguration;  
    String CreatedBy;  
    String CustomBootImagePackage_x64;  
    String CustomBootImagePackage_x86;  
    DateTime DateCreated;  
    DateTime DateEnded;  
    DateTime DateLastUpdated;  
    DateTime DateNextRun;  
    DateTime DateStarted;  
    String Description;  
    String DestinationSiteCode;  
    String DestinationSiteFQDN;  
    Boolean DisableAdvertisements;  
    UInt32 FailedObjectNumber;  
    UInt32 JobID;  
    String JobName;  
    UInt32 MigratedObjectNumber;  
    Boolean MigrateWithFolders;  
    String ModifiedBy;  
    UInt32 ResolveObjectConflictOption;  
    String ScheduleToken;  
    String ScopeIDs[];  
    UInt32 SkippedObjectNumber;  
    String SourceCollectionIDs[];  
    UInt32 SourceObjectIDs[];  
    String SourceSiteCode;  
    String SourceSiteFQDN;  
    UInt32 SourceSiteID;  
    UInt32 Status;  
    UInt32 TotalObjectNumber;  
    UInt32 Type;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_MigrationJob` class.  

|Method|Description|  
|------------|-----------------|  
|[Start Method in Class SMS_MigrationJob](../../../../develop/reference/core/migration/start-method-in-class-sms_migrationjob.md)|Starts the migration job.|  
|[Stop Method in Class SMS_MigrationJob](../../../../develop/reference/core/migration/stop-method-in-class-sms_migrationjob.md)|Stops the migration job.|  

## Properties  
 `AdditionalConfiguration`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Additional configuration for migration jobs.  

 For a collection migration job, the configuration contains the collections information included in this job. The format is like:  

```  
<MigrationJob>  
   <Collection ID="JQX00011" Type="2" LimitTo="SMS00019" />  
   <Collection ID="JQX00012" Type="2" />  
   <Collection ID="JQX00018" Type="2" />  
   <SiteCodeMap Old="JQX" New="CAR" />  
   <SiteCodeMap Old="P5P" New="PE1" />  
   </Collection>  
</MigrationJob>   
```  

 For a distribution point upgrade job, the configuration contains the settings to upgrade a shared distribution point. The format is like:  

```  
<DPUpgrade>  
  <SourceSiteCode>CEN</SourceSiteCode>  
  <SiteCode>CAS</SiteCode>  
  <NALPath>…</NALPath>  
  …  
  <SiteSystem>  
    <NALPath>…</NALPath>  
    …  
    <EmbeddedProperties>  
      <EmbeddedProperty>  
        <PropertyName>IsProtected</PropertyName>  
        <Value>0</Value>  
        <Value1 />  
        <Value2 />  
      </EmbeddedProperty>  
      …  
    </EmbeddedProperties>  
  </SiteSystem>  
  <DistributionPoint>  
  …  
  </DistributionPoint>  
</DPUpgrade>  
```  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the user who created this job.  

 `CustomBootImagePackage_x64`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 PackageID of a boot image package to use for x64 boot images in place of the default.  

 `CustomBootImagePackage_x86`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 PackageID of a boot image package to use for x86 boot images in place of the default.  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time that the job was created.  

 `DateEnded`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time that the job ended.  

 `DateLastUpdated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time that the job was last updated.  

 `DateNextRun`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time that the job will run next.  

 `DateStarted`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Time that the job started.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the job.  

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

 `DisableAdvertisements`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if migrated advertisements will be disabled.  

 `FailedObjectNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of failed objects.  

 `JobID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifier of the job.  

 `JobName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the job.  

 `MigratedObjectNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of migrated objects.  

 `MigrateWithFolders`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` if the folder structure should be migrated along with the objects.  

 `ModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Name of the user who most recently modified this job.  

 `ResolveObjectConflictOption`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Resolve object conflict option.  

 `ScheduleToken`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Schedule token, writable only with the manage migration Job right..  

 `ScopeIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Scope IDs that migrated entities should be in.  

 `SkippedObjectNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of skipped objects.  

 `SourceCollectionIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Source collection IDs selected for migration.  

 `SourceObjectIDs`  
 Data type: `UInt32 Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Source object IDs included in the job.  

 `SourceSiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Source site code.  

 `SourceSiteFQDN`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Source site FQDN.  

 `SourceSiteID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Source site ID.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, read]  

 Job status. Possible values are:  

|||  
|-|-|  
|0|NotStarted|  
|1|Completed|  
|2|Running|  
|3|Failed|  
|4|Stopped|  

 `TotalObjectNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Number of objects.  

 `Type`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 The type of job. Possible values are:  

|||  
|-|-|  
|1|Object|  
|2|Client|  
|3|ObjectandClient|  

## Remarks  
 Migration jobs are the object used by the server components to perform a migration task. There are three types of migration jobs: 1) collection migration job, 2) object migration job and 3) distribution point upgrade job. Job types are defined using the `Type` property.  

 Collection migration jobs include the collections and collection related information such as the limiting collection, the source site code and the destination site code. Object migration jobs can include objects such as packages, but cannot include the collections and the targeting objects such as advertisements. Distribution point upgrade jobs can upgrade a shared distribution point to a System Center Configuration Manager regular distribution point.  

 For collection migration jobs and object migration jobs, the included objects’ entity ID is stored as an array of properties on the job, SourceCollectionIDs and SourceObjectIDs. For distribution point upgrade jobs, the settings for the new site system and distribution point are stored as XML in the property `AdditionalConfiguration`. All job types are scheduled by using the `ScheduleToken` property.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
