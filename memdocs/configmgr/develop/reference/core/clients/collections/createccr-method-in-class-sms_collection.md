---
description: Learn how to create a client configuration request (CCR) for a particular resource in Configuration Manager.
title: "CreateCCR Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 2127929c-6a20-457d-a351-5c3262363430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# CreateCCR Method in Class SMS_Collection
The `CreateCCR` Windows Management Instrumentation (WMI) class method creates a client configuration request (CCR) for a particular resource.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 CreateCCR(  
     UInt32 ResourceID,  
     Boolean PushOnlyAssignedClients,  
     SInt32 ClientType,  
     Boolean Forced,  
     Boolean ForceReinstall,  
     Boolean PushEvenIfDC,  
     Boolean InformationOnly,  
     Boolean SpecifySiteCode,   
     String PushSiteCode)  

```  

#### Parameters  
 `ResourceID`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 ID of a member resource.  

 `PushOnlyAssignedClients`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 This property is deprecated.  

 `ClientType`  
 This property is deprecated.  

 `Forced`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` to force installation. This defaults to `false`, if not specified. This is used for force reinstallation, even if the client is already installed. If set to `true`, the operating system will be ignored.  

 `ForceReinstall`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` to force reinstallation. The value defaults to false, if not specified.  

 `PushEvenIfDC`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` to push installation on a domain component. The value defaults to false, if not specified.  

 `InformationOnly`  
 Data type: `Boolean`  

 Qualifiers: [in, optional]  

 `true` if the CCR is for information only. This parameter is only used to gather information from the client. The value defaults to false, if not specified.  

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
