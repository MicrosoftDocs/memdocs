---
title: "ResolveConflict Method"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the ResolveConflict Windows Management Instrumentation class method is used to resolve conflicts that result by creating or editing software entries, and the same software entry created by Microsoft through the online synchronization."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: b58c5608-7db3-407f-a981-d0e411d06964
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ResolveConflict Method in Class SMS_AISoftwareList
The `ResolveConflict` Windows Management Instrumentation (WMI) class method, in Configuration Manager, is used to resolve conflicts that result by creating or editing software entries, and the same software entry being created by Microsoft through the online synchronization.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 ResolveConflict(      
     String SoftwareKey,  
     UInt32 Resolution  
);  
```  

#### Parameters  
 `SoftwareKey`  
 Data type: `String`  

 Qualifiers: [in]  

 The MD5 hash of the software entry, which has a conflict to be resolved. The hash is made up of the software name, publisher, and version.  

 This property name has changed from `SoftwarePropertiesHash` to `SoftwareKey` in SP1.  

 `Resolution`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Action to take on the software entry.  

|Value|Description|  
|-----------|-----------------|  
|1|Keep the local copy and discard any updates from Microsoft.|  
|2|Revert the local copy and replace it with latest update from Microsoft.|  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_AISoftwareList Server WMI Class](../../../../../develop/reference/core/clients/asset-intelligence/sms_aisoftwarelist-server-wmi-class.md)
