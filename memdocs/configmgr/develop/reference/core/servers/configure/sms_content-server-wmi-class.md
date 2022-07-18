---
title: "SMS_Content Class"
description: Learn how the SMS_Content class is an SMS Provider server class, in Configuration Manager, that provides additional information about a CI_Content instance.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 8973d915-1d74-46cd-a20d-a19de59a677a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Content Server WMI Class
The `SMS_Content` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that provides additional information about a `CI_Content` instance.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Content : SMS_BaseClass  
{  
    String ContentDescription;  
    UInt32 ContentFlags;  
    String ContentHash;  
    UInt32 ContentHashVersion;  
    SInt32 ContentID;  
    String ContentSource;  
    UInt32 ContentType;  
    String ContentUniqueID;  
    UInt32 ContentVersion;  
    UInt32 ObjectTypeID;  
    String RelatedContentID;  
    String SecurityKey;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_Content` class.  

|Method|Description|  
|------------|-----------------|  
|[IsOfficeContent Method in Class SMS_Content](../../../../../develop/reference/core/servers/configure/isofficecontent-method-in-class-sms_content.md)|Specifies whether content is Microsoft Office content.|  

## Properties  
 `ContentDescription`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the content.  

 `ContentFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 This specifies additional attributes for content instance.  

|Value|Content flag|  
|-|-|  
|8|DOWNLOAD_ON_DEMAND_FROM_LOCAL_DP|  
|12|DOWNLOAD_FROM_LOCAL_DISPPOINT|  
|13|DOWNLOAD_LOCAL_PARTIALDOWNLOADTOLOCAL|  
|14|DOWNLOAD_FROM_REMOTE_DISPPOINT|  
|15|DOWNLOAD_REMOTE_PARTIALDOWNLOADTOLOCAL|  
|16|DOWNLOAD_ENABLE_PEER_CACHING|  
|17|DP_NO_FALLBACK_UNPROTECTED|  
|24|DO_NOT_DOWNLOAD|  
|25|PERSIST_IN_CACHE|  

 `ContentHash`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Hash of the content.  

 `ContentHashVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 This specifies the hash version used to calculate the content hash.  

 `ContentID`  
 Data type: `SInt32`  

 Access type: Read-only  

 Qualifiers: [key, read]  

 Identifier for the content.  

 `ContentSource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 This specifies the source location where content files are stored.  

 `ContentType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Type of the content.  

 `ContentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Unique identifier for the content.  

 `ContentVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Version of the content.  

 `ObjectTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The security type of the content.  

 `RelatedContentID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Specifies the related content associated with this content.  

 `SecurityKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The security key of the content. Content may be secured by application or package.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
