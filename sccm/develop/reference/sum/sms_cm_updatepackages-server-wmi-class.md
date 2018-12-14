---
title: "SMS_CM_UpdatePackages Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 18ca108c-5c3c-4022-b72b-b3a62ce53549
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_CM_UpdatePackages Server WMI Class
The  `SMS_CM_UpdatePackages` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents update packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_UpdatePackages : SMS_BaseClass  
{  
    String ClientVersion;  
    DateTime DateCreated;  
    DateTime DateReleased;  
    String Description;  
    String EULA;  
    String FullVersion;  
    SInt32 Impact;  
    DateTime LastUpdateTime;  
    SInt32 LocaleID;  
    String MaxCMVersion;  
    String MinCMVersion;  
    String MoreInfoLink;  
    String Name;  
    String PackageGuid;  
    Sint32 PrereqFlag;  
    String PrereqPackageName;   
    SInt32 PrereqPackageState;  
    SInt32 PublisherFlags;  
    SInt32 State;  
    SInt32 UpdateType;  
    SInt32 WarningFlag;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_CM_UpdatePackages` class.  

|Method|Description|  
|------------|-----------------|  
|[IsCurrentWorkingUpdatePackage Method in Class SMS_CM_UpdatePackages](../../../develop/reference/sum/iscurrentworkingupdatepackage-method-in-class-sms_cm_updatepackages.md)|Checks whether the update package is the package that setup is currently working on|  
|[RetryContentReplication Method in Class SMS_CM_UpdatePackages](../../../develop/reference/sum/retrycontentreplication-method-in-class-sms_cm_updatepackages.md)|Triggers DistMgr to copy content from the source to the content library.|  
|[SetIgnorePrereqWarning Method in Class SMS_CM_UpdatePackages](../../../develop/reference/sum/setignoreprereqwarning-method-in-class-sms_cm_updatepackages.md)|Updates the ignore pre-requisites warning flag of the update packages.|  
|[UpdatePrereqAndStateFlags Method in Class SMS_CM_UpdatePackages](../../../develop/reference/sum/updateprereqandstateflags-method-in-class-sms_cm_updatepackages.md)|Updates the installation state of update packages.|  

## Properties  
 `ClientVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The client version, if there is a client update in the package.  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The date  the update package was added to the site.  

 `DateReleased`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The date the update package was released.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 A description of the update package.  

 `EULA`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The Microsoft Software License Terms for the overall update package.  

 `FullVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The full version.  

 `Impact`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Bit to indicate impact. Possible values are:  

|||  
|-|-|  
|0x01|Site server|  
|0x02|Console|  
|0x04|Client|  
|0x08|New features|  
|0x10|Bug fixes|  

 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The date and time that the state was last updated.  

 `LocaleID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The locale ID for the localized data.  

 `MaxCMVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The maximum applicable version of Configuration Manager.  

 `MinCMVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The minimum applicable version of Configuration Manager.  

 `MoreInfoLink`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Link to additional information about the update package.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the update package.  

 `PackageGuid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 A unique identifier for the feature.  

 `PrereqFlag`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Flag for pre-requisites. Valid values are:  

|||  
|-|-|  
|0x1|Prereq only|  
|0x2|CONTINUE_ON_PREREQ_WARNING|  

 `PrereqPackageName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The name of the package that the current package depends on.  

 `PrereqPackageState`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The state of the package that the current package depends on.  

 `PublisherFlags`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 0x2: update boot image package.  

 `State`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The overall state of the update package.  

 `UpdateType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Package type. Possible values are:  

|||  
|-|-|  
|0|Regular Update|  
|1|Weave|  
|2|QFE|  

 `WarningFlag`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Warning flag. Possible values are:  

|||  
|-|-|  
|0|Bypass warning|  
|1|Do not bypass warning|  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
