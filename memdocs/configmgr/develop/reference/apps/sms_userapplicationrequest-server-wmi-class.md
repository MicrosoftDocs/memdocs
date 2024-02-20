---
title: SMS_UserApplicationRequest Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the SMS_UserApplicationRequest WMI class is an SMS Provider server class that represents a user's application request.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 74290916-947a-432f-ab33-cbf7358ee126
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_UserApplicationRequest Server WMI Class
The `SMS_UserApplicationRequest` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a user's application request.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_UserApplicationRequest :    
{  
    String Application;  
    String CI_UniqueID;  
    String Comments;  
    UInt32 CurrentState;  
    String LastModifiedBy;  
    DateTime LastModifiedDate;  
    String ModelName;  
    String RequestGuid;  
    SMS_UserApplicationRequestHistoryItem RequestHistory[];  
    String User;  
    String UserSid;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_UserApplicationRequest` class.  

|Method|Description|  
|------------|-----------------|  
|[Approve Method in Class SMS_UserApplicationRequest](../../../develop/reference/apps/approve-method-in-class-sms_userapplicationrequest.md)|Approves a user application request.|  
|[Deny Method in Class SMS_UserApplicationRequest](../../../develop/reference/apps/deny-method-in-class-sms_userapplicationrequest.md)|Denies a user application request.|  

## Properties  
 `Application`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the application.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Unique ID of the configuration item. This ID is unique across sites.  

 `Comments`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Last set of comments for the request.  

 `CurrentState`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Current state of the application request. Possible values are:  

|Value|Current state|  
|-|-|  
|1|Requested|  
|2|Canceled|  
|3|Denied|  
|4|Approved|  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User who last modified the request.  

 `LastModifiedDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Date and time for the last modification of this request.  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Model name of the requested application.  

 `RequestGuid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique GUID for the request.  

 `RequestHistory`  
 Data type: `SMS_UserApplicationRequestHistoryItem Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 History of the request, one entry per update that was done.  

 `User`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 User that requested the application.  

 `UserSid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Security identifier of the user that requested the application.  

## Remarks  

## Requirements  
 A user application request is unique for a given user and application.  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
