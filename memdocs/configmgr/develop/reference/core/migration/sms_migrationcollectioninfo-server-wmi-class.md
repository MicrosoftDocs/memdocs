---
title: "SMS_MigrationCollectionInfo Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4e8a8dbb-bf0a-4331-846c-0f121bb396ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_MigrationCollectionInfo Server WMI Class
The `SMS_MigrationCollectionInfo` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the collections created on the current active Configuration Manager 2007 hierarchy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MigrationCollectionInfo : SMS_BaseClass  
{  
    UInt32 ChildCount;  
    String Children;  
    UInt32 CollectionEntityID;  
    String CollectionName;  
    UInt32 CollectionType;  
    UInt32 Count;  
    Boolean IsTop;  
    UInt32 LimitToCount;  
    String LimitTos;  
    UInt32 SiteCodeCount;  
    String SiteCodes;  
    String SourceSiteCollectionID;  
    UInt32 SourceSiteID;  
    UInt32 Status;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_MigrationCollectionInfo` class.  

|Method|Description|  
|------------|-----------------|  
|[GetClientsCountByCollections Method in Class SMS_MigrationCollectionInfo](../../../../develop/reference/core/migration/getclientscountbycollections-method-in-class-sms_migrationcollectioninfo.md)|Retrieves the number of clients in the specified collection. **Warning:**  This method is reserved for future use.|  

## Properties  
 `ChildCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The count of child collections.  

 `Children`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The child collection Ids, separated by ','.  

 `CollectionEntityID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Entity ID of this collection.  

 `CollectionName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 Display name of the collection.  

 `CollectionType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The type of the collection.  

|Value|Collection type|  
|-|-|  
|0|Mixed|  
|1|User|  
|2|Device|  
|3|UnknownArchitecture|  
|4|UnknownQuery|  
|5|Folder|  

 `Count`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The total number of devices or users in this collection.  

 `IsTop`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: none  

 `true` if the collection is a top collection which linked to the root.  

 `LimitToCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The total number of collections that the collection is limited to.  

 `LimitTos`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The string that concatenate all ID of collections that the collection is limit to, separated by ','.  

 `SiteCodeCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 The count of site codes embedded in the query.  

 `SiteCodes`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: none  

 The string that concatenate all site codes that embedded in the collection query string, separated by ','.  

 `SourceSiteCollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key]  

 Unique identifier for the collection in the source site.  

 `SourceSiteID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 Unique identifier for the source site in `SMS_MigrationSourceSite`.  

 `Status`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: none  

 Status of the collection.  

## Remarks  
 Each instance of this class represents a collection.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../develop/core/reqs/server-development-requirements.md).
