---
title: "GetAutoUpgradeConfigs Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 01ad5660-fcae-4e18-bafd-453caa15bc30
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# GetAutoUpgradeConfigs Method in Class SMS_Site
The `GetAutoUpgradeConfigs` Windows Management Instrumentation (WMI) class method, in Configuration Manager, gets configurations for auto-upgrade settings.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
SInt32 GetAutoUpgradeConfigs(  
     String ClientVersion,  
     Boolean IsProgramEnabled,  
     UInt32 AdvertisementDuration,  
     UInt32 ValidationInterval,  
     UInt32 ValidationFailureInterval,  
     Boolean AllowPrestage,  
     Boolean AllowFallbackToContentSource,  
     UInt32 DownloadOptionsInSlowNetwork,  
     Boolean ExcludeServers,  
     Boolean OverrideServiceWindow,  
     Boolean IgnoreNonPersistableVM,  
     Boolean IsInitialized  
     DateTime LastModifiedTime,  
     String LastModifiedBy  
);  
```  

#### Parameters  
 `ClientVersion`  
 Data type: `String`  

 Qualifiers: [out]  

 The version of the client.  

 `IsProgramEnabled`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if the program is enabled.  

 `AdvertisementDuration`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Advertisement duration in days.  

 `ValidationInterval`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Validation interval in hours, if the previous validation is successful.  

 `ValidationFailureInterval`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Validation interval in hours, if the previous validation is failed.  

 `AllowPrestage`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if auto-upgrade package distributed to pre-stage distribution point is allowed.  

 `AllowFallbackToContentSource`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if fallback to content source is allowed.  

 `DownloadOptionInSlowNetwork`  
 Data type: `UInt32`  

 Qualifiers: [out]  

 Download options in slow network. Possible values are:  

|Value|Download option|  
|-|-|  
|0|Do not download.|  
|1|Download from distribution point and run locally.|  
|2|Run from distribution point.|  

 `ExcludeServers`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 Indicates whether auto-upgrade should be skipped on servers.  

 `OverrideServiceWindow`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 Indicates whether the upgrade on the client will occur in service window.  

 `IgnoreNonPersistableVM`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 Indicates whether auto-upgrade should be skipped on non-persistent virtual machines.  

 `IsInitialized`  
 Data type: `Boolean`  

 Qualifiers: [out]  

 `true` if auto-upgrade settings are initialized.  

 `LastModifiedTime`  
 Data type: `DateTime`  

 Qualifiers: [out]  

 Last modified time.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

 `LastModifiedBy`  
 Data type: `String`  

 Qualifiers: [out]  

 The name of the user that made the last modification.  

 This information applies to System Center 2012 Configuration Manager SP1 or later, and System Center 2012 R2 Configuration Manager or later.  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Site Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)
