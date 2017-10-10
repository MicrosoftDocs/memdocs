---
title: "SMS_MDMAppleVppToken Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 38903d4e-d6de-4209-8c36-db66d8822e36searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MDMAppleVppToken Server WMI Class
The `SMS_MDMAppleVppToken` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an Apple Volume Purchase Program (VPP) token.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMAppleVppToken : SMS_BaseClass  
{  
    DateTime Created;  
    String Description;  
    DateTime ExpirationDate;  
    String Id;  
    DateTime LastSuccessfulSync;  
    DateTime LastSync;  
    DateTime LastUpdated;  
    String Name;  
    String OrganizationName;  
    String SyncErrorCode;  
    DateTime SyncStartTime;  
    SInt32 SyncStatus;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_MDMAppleVppToken` class.  

|Method|Description|  
|------------|-----------------|  
|[SyncToken Method in Class SMS_MDMAppleVppToken](../../../develop/reference/mdm/synctoken-method-in-class-sms_mdmapplevpptoken.md)|Initiates a synchronization of an Apple VPP token.|  
|[UploadToken Method in Class SMS_MDMAppleVppToken](../../../develop/reference/mdm/uploadtoken-method-in-class-sms_mdmapplevpptoken.md)|Uploads an Apple VPP token to Intune.|  

## Properties  
 `Created`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Date the token was created.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description of the token.  

 `ExpirationDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 Expiration date of the token.  

 `Id`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 The token ID.  

 `LastSuccessfulSync`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The last time a synchronization with Apple was successful.  

 `LastSync`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The last time a synchronization with Apple occurred.  

 `LastUpdated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The last time the token was updated.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the token.  

 `OrganizationName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Organization name for the token.  

 `SyncErrorCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Error code for a synchronization error.  

 `SyncStartTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The time when a synchronization was initiated.  

 `SyncStatus`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Status of the current or last synchronization.  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Mobile Device Management Server WMI Classes](../../../develop/reference/mdm/mobile-device-management-server-wmi-classes.md)   
 [Configuration Manager Hybrid Server WMI Classes](../../../develop/reference/mdm/hybrid-server-wmi-classes.md)
