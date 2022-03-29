---
description: Article describing the use of CreateCCRs in Configuration Manager to generate client configuration requests for the computers in the collection.
title: CreateCCRs method in class SMS_Collection
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4c3288fd-a973-4300-b9c5-475867c26fc5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CreateCCRs Method in Class SMS_Collection
The `CreateCCRs` WMI class method, in Configuration Manager, generates client configuration requests (CCRs) for the computers in the collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CreateCCRs(  
     Boolean IncludeSubCollections,  
     Boolean PushOnlyAssignedClients,  
     SInt32 ClientType,  
     Boolean Forced,  
     Boolean ForceReinstall,  
     Boolean PushEvenIfDC,  
     Boolean InformationOnly  
     Boolean SpecifySiteCode,   
     String PushSiteCode)   
);  
```  

#### Parameters  
 `IncludeSubCollections`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` to include subcollections. This defaults to false, if not specified.  

 `PushOnlyAssignedClients`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 This property is deprecated.  

 `ClientType`  
 This property is deprecated.  

 `Forced`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` to force installation. This defaults to false, if not specified. This is used for force reinstallation, even if the client is already installed. If set to `true`, the operating system will be ignored.  

 `ForceReinstall`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` to force reinstallation. This defaults to false, if not specified.  

 `PushEvenIfDC`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` to push installation on a domain component. This defaults to false, if not specified.  

 `InformationOnly`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` if the CCRs are for information only. This parameter is only used to gather information from the client. This defaults to false, if not specified.  

 `SpecifySiteCode`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `SpecifySiteCode` is used to control whether the `PushSiteCode` parameter is used. If `SpecificySiteCode` is set to `true`, `PushSiteCode` will be used. If `SpecificySiteCode` is not set to `true`, `PushSiteCode` will not be used.  

 `PushSiteCode`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `PushSiteCode` defines which site will initiate the actual push. The specified site will push its client files to the client and do the actual installation.  

## Return Values  
 An  `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Collection Server WMI Class](../../../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)   
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
