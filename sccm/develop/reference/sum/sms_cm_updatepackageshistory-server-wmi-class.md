---
title: "SMS_CM_UpdatePackagesHistory Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d22e5e14-7035-4c8f-ad2a-1cf9475214f8searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CM_UpdatePackagesHistory Server WMI Class
The `SMS_CM_UpdatePackagesHistory` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that is used to get a list of all update packages.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_UpdatePackagesHistory: SMS_BaseClass  
{  
    String ClientVersion;  
    DateTime DateCreated;  
    DateTime DateReleased;  
    String Description;  
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
 The `SMS_CM_UpdatePackagesHistory` class does not define any methods.  

## Properties  
 `ClientVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The client version, if there is a client update in the package.  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The date  the update package was added to the site.  

 `DateReleased`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The date the update package was released.  

 `Description`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 A description of the update package.  

 `FullVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The full version.  

 `Impact`  
 Data type: `SInt32`  

 Access type: Read  

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

 Access type: Read  

 Qualifiers: none  

 The date and time that the state was last updated.  

 `LocaleID`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 The locale ID for the localized data.  

 `MaxCMVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The maximum applicable version of Configuration Manager.  

 `MinCMVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The minimum applicable version of Configuration Manager.  

 `MoreInfoLink`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Link to additional information about the update package.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The name of the update package.  

 `PackageGuid`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 A unique identifier for the package.  

 `PrereqFlag`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 Flag for pre-requisites. Valid values are:  

|||  
|-|-|  
|0x1|Prereq only|  
|0x2|CONTINUE_ON_PREREQ_WARNING|  

 `PrereqPackageName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The name of the package that the current package depends on.  

 `PrereqPackageState`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 The state of the package that the current package depends on.  

 `PublisherFlags`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 0x2: update boot image package.  

 `State`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 The overall state of the update package.  

 `UpdateType`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 Package type. Possible values are:  

|||  
|-|-|  
|0|Regular Update|  
|1|Weave|  
|2|QFE|  

 `WarningFlag`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 Warning flag. Possible values are:  

|||  
|-|-|  
|0|Bypass warning|  
|1|Do not bypass warning|  

## Remarks  
 Class qualifiers for this class include:  

-   Dynamic  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
