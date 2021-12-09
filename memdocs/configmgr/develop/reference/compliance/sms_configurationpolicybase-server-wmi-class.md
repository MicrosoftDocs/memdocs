---
title: "SMS_ConfigurationPolicyBase Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7a8c1139-a0cc-4b5a-9173-9b849068cf16
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ConfigurationPolicyBase Server WMI Class
The `SMS_ConfigurationPolicyBase` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents the base class for configuration policy.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigurationPolicyBase : SMS_ConfigurationItemBaseClass  
{  
    UInt32 ActivatedCount;  
    String ApplicabilityCondition;  
    UInt32 AssignedCount;  
    String CategoryInstance_UniqueIDs[];  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    UInt32 CIType_ID;  
    UInt32 CIVersion;  
    UInt32 ComplianceCount;  
    Real64 CompliantPercentage;  
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
    UInt32 FailureCount;  
    Boolean IsAssigned;  
    Boolean IsBroken;  
    Boolean IsBundle;  
    Boolean IsDigest;  
    Boolean IsEnabled;  
    Boolean IsExpired;  
    Boolean IsHidden;  
    Boolean IsLatest;  
    Boolean IsQuarantined;  
    Boolean IsSuperseded;  
    Boolean IsUserDefined;  
    String LastModifiedBy;  
    String LocalizedCategoryInstanceNames[];  
    String LocalizedDescription;  
    String LocalizedDisplayName;  
    SMS_CI_LocalizedEulas LocalizedEulas[];  
    SMS_CI_LocalizedProperties LocalizedInformation[];  
    String LocalizedInformativeURL;  
    UInt32 LocalizedPropertyLocaleID;  
    UInt32 ModelID;  
    String ModelName;  
    UInt32 NonComplianceCount;  
    UInt32 PermittedUses;  
    String PlatformCategoryInstance_UniqueIDs[];  
    UInt32 PlatformType;  
    UInt32 Precedence;  
    SMS_SDMPackageLocalizedData SDMPackageLocalizedData[];  
    UInt32 SDMPackageVersion;  
    String SDMPackageXML;  
    String SecuredScopeNames[];  
    String SedoObjectVersion;  
    UInt32 Severity;  
    String SourceSite;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_ConfigurationPolicyBase` class.  

|Method|Description|  
|------------|-----------------|  
|[AcceptEULA Method in Class SMS_ConfigurationPolicyBase](../../../develop/reference/compliance/accepteula-method-in-class-sms_configurationpolicybase.md)|Accepts or declines the Microsoft Software License Terms of a configuration item.|  
|[GetEULA Method in Class SMS_ConfigurationPolicyBase](../../../develop/reference/compliance/geteula-method-in-class-sms_configurationpolicybase.md)|Gets the localized Microsoft Software License Terms content, if a configuration item is present.|  

## Properties  
 `ActivatedCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The number of computers that have evaluated the configuration policy item.  

 `ApplicabilityCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, sizelimit]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `AssignedCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The number of computers or users that have been assigned this configuration policy item.  

 `CategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, key]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null, unique]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CIType_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [enumeration, not_null, read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ComplianceCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Number of computers that are compliant with the configuration item.  

 `CompliantPercentage`  
 Data type: `Real64`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The property is deprecated.  

 `ConfigurationFlags`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, sizelimit]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `DateLastModified`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `EffectiveDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `EULAAccepted`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `EULAExists`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `EULASignoffDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `EULASignoffUser`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ExecutionContext`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, valuemap, values]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `FailureCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Represents the number of targets that reported an error during configuration policy evaluation.  

 `IsAssigned`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 `true` if this is an assigned policy.  

 `IsBroken`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsBundle`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsDigest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsExpired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsHidden`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsLatest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsQuarantined`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsSuperseded`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsUserDefined`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read, sizelimit]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedEulas`  
 Data type: `SMS_CI_LocalizedEulas Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedInformation`  
 Data type: `SMS_CI_LocalizedProperties Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedInformativeURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ModelID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `NonComplianceCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 Number of computers that are not compliant with the configuration item.  

 `PermittedUses`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `PlatformCategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `PlatformType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bitmap, bitvalues, read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `Precedence`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Precedence represents a resolution order to resolve conflicting rules detected by the rules engine on the client. Currently this is only applicable to EP Firewall configuration policies.  

 `SDMPackageLocalizedData`  
 Data type: `SMS_SDMPackageLocalizedData Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `SDMPackageXML`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `SecuredScopeNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `Severity`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 The non-compliance severity of the configuration item.  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [sizelimit]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
