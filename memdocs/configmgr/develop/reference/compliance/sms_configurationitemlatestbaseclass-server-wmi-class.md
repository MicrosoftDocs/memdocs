---
title: SMS_ConfigurationItemLatestBaseClass Class
titleSuffix: Configuration Manager
description: An SMS Provider server class, in Configuration Manager, that represents the latest version of Configuration Items in the system.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: c31f0f2e-09f6-41e6-ac20-622080053b73
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_ConfigurationItemLatestBaseClass Server WMI Class
The `SMS_ConfigurationItemLatestBaseClass` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the latest version of Configuration Items in the system.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigurationItemLatestBaseClass : SMS_BaseClass  
{  
    String ApplicabilityCondition;  
    String CategoryInstance_UniqueIDs[];  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    UInt32 CIType_ID;  
    UInt32 CIVersion;  
    UInt64 ConfigurationFlags;  
    String CreatedBy;  
    DateTime DateCreated;  
    DateTime DateLastModified;  
    DateTime EffectiveDate;  
    UInt32 EULAAccepted;  
    Boolean EULAExists;  
    DateTime EULASignoffDate;  
    String EULASignoffUser;  
    UInt32 ExecutionContext;  
    Boolean IsBundle;  
    Boolean IsDigest;  
    Boolean IsEnabled;  
    Boolean IsExpired;  
    Boolean IsHidden;  
    Boolean IsLatest;  
    Boolean IsSuperseded;  
    Boolean IsUserDefined;  
    String LastModifiedBy;  
    String LocalizedCategoryInstanceNames[];  
    String LocalizedDescription;  
    String LocalizedDisplayName;  
    String LocalizedInformativeURL;  
    UInt32 LocalizedPropertyLocaleID;  
    UInt32 ModelID;  
    String ModelName;  
    UInt32 PermittedUses;  
    String PlatformCategoryInstance_UniqueIDs[];  
    UInt32 PlatformType;  
    SMS_SDMPackageLocalizedData SDMPackageLocalizedData[];  
    UInt32 SDMPackageVersion;  
    String SDMPackageXML;  
    String SecuredScopeNames[];  
    String SedoObjectVersion;  
    String SourceSite;  
};  
```  

## Methods  
 The `SMS_ConfigurationItemLatestBaseClass` class does not define any methods.  

## Properties  
 `ApplicabilityCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, sizelimit("512")]  

 Condition that the client evaluates before evaluating the configuration item targeted by an assignment. If the condition does not exist, the configuration item is not evaluated on the client. The string can contain up to 512 characters.  

 `CategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 The unique IDs of the categories to which the configuration item belongs.  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The unique ID of the configuration item. This ID is unique only for the site.  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, unique]  

 The unique ID of the configuration item. This ID is unique across sites.  

 `CIType_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, not_null, read]  

 The type of the configuration item. Possible values are:  

|Value|Configuration item type|  
|-|-|  
|1|SoftwareUpdate|  
|2|Baseline|  
|3|OperatingSystem|  
|4|BusinessPolicy (General)|  
|5|Application|  
|6|Driver|  
|7|OtherConfigurationItem|  
|8|SoftwareUpdateBundle|  
|9|AuthorizationList (SoftwareUpdateAuthorizationList)|  
|10|AppModel|  
|11|GlobalSettings|  
|13|GlobalExpression|  
|14|Platform|  
|21|DeploymentType|  
|24|Install Policy Type|  
|25|DeploymentTechnology|  
|26|HostingTechnology|  
|27|InstallerTechnology|  
|28|PublishingItem|  
|29|ApplicationGroup|  
|40|SettingsDefinition|  
|50|ConfigurationPolicy|  
|60|VirtualEnvironment|  
|70|AbstractConfigurationItem|  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Configuration item policy version, which is automatically incremented.  

 `ConfigurationFlags`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [bits("COMPLIANCE_POLICY(0)"), read]  

 A bitmask for additional properties,  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, sizelimit("512")]  

 Name of the user who created the configuration item.  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Date and time when the configuration item was created.  

 `DateLastModified`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the configuration item was last modified.  

 `EffectiveDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the <!-- Network Access Protection (NAP)  -->compliance policy for the configuration item becomes effective.  

 `EULAAccepted`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Indication of acceptance of the Microsoft Software License Terms for the configuration item. The default value is 2.  

 Possible values are:  

|Value|License terms acceptance|  
|-|-|  
|0|Declined|  
|1|Accepted|  
|2|Undetermined (default)|  

 `EULAExists`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if Microsoft Software License Terms exist. The default value is `false`.  

 `EULASignoffDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 Date and time when the Microsoft Software License Terms were signed off.  

 `EULASignoffUser`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 User who signed off on the Microsoft Software License Terms.  

 `ExecutionContext`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, valuemap, values]  

 Execution context that the configuration item should be evaluated under.  

|Value|Execution context|  
|-|-|  
|0|System|  
|1|User|  

 `IsBundle`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the configuration item is bundled within another configuration item.  

 `IsDigest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 Deprecated.  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the configuration item is enabled and can be evaluated.  

 `IsExpired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the configuration item is no longer active.  

 `IsHidden`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the configuration item is not shown in the Configuration Manager console.  

 `IsLatest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the configuration item is the latest.  

 `IsSuperseded`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if the configuration item is superseded by a new configuration item.  

 `IsUserDefined`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if the configuration item was created by the user.  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, sizelimit("512")]  

 User who last modified the configuration item. The string can contain up to 512 characters.  

 `LocalizedCategoryInstanceNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized names of the categories to which the configuration item belongs.  

 `LocalizedDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized description of the configuration item.  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 Localized display name of the configuration item.  

 `LocalizedInformativeURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 URL for additional localized information about the configuration item.  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Locale ID of the localized properties of the configuration item.  

 `ModelID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 The model ID.

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, not_null, unique]  

 Desired configuration management model name for the configuration item.  

 `PermittedUses`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Valid uses of the configuration item.  

 `PlatformCategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 Category of the platform that this configuration item is applicable on.  

 `PlatformType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bitmap, bitvalues, read]  

 Platform that the configuration item is applicable on.  

 `SDMPackageLocalizedData`  
 Data type: `SMS_SDMPackageLocalizedData Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Localized data files associated with the System Definition Model (SDM) package for the configuration item.  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Deprecated.  

 `SDMPackageXML`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The DCM digest of the configuration item if it is a fully interpreted configuration item. This property indicates the Service Modeling Language (SML) definition of the configuration item if it is an item that is not interpreted or partially interpreted.  

 `SecuredScopeNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 The names of the secured scopes.

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

The version of the SEDO object.

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit("3")]  

 Site where the configuration item is imported or created. The string can contain up to three characters.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
