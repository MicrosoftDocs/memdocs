---
title: "UpdateClientPilotingConfigs Method"
titleSuffix: "Configuration Manager"
description: "UpdateClientPilotingConfigs, in Configuration Manager, updates the configurations for client piloting settings."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 970cb1ba-ee11-459c-9c59-cf2c992cbbab
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# UpdateClientPilotingConfigs Method in Class SMS_Site
The `UpdateClientPilotingConfigs` Windows Management Instrumentation (WMI) class method, in Configuration Manager, updates the  configurations for client piloting settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 UpdateClientPilotingConfigs (  
    Boolean IsEnabled,  
    Boolean IsAccepted,  
    String TargetCollectionID  
);  

```  

#### Parameters  
 `IsEnabled`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 Indicates whether client piloting testing mode is enabled.  

 `IsAccepted`  
 Data type: `Boolean`  

 Qualifiers: [in]  

 Indicates whether the new client binaries are accepted. If `IsEnabled` is `true`, this parameter is ignored and is always `false`.  

 `TargetCollectionID`  
 Data type: `String`  

 Qualifiers: [in]  

 Targeted collection ID.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For more information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
