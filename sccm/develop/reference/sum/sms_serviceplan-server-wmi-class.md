---
title: "SMS_ServicePlan Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5a387a79-8915-4f09-a354-96da17798a89searchScope: - ConfigMgr SDK
caps.latest.revision: 3
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ServicePlan Server WMI Class
The `SMS_ServicePlan` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a service plan.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ServicePlan : SMS_SoftwareUpdateBase  
{  
    String ApplicabilityCondition;  
    String ArticleID;  
    String BulletinID;  
    String CategoryInstance_UniqueIDs[];  
    UInt32 CI_ID;  
    String CI_UniqueID;  
    UInt32 CIType_ID;  
    UInt32 CIVersion;  
    UInt64 ConfigurationFlags;  
    String CreatedBy;  
    UInt32 CustomSeverity;  
    String CustomSeverityName;  
    DateTime DateCreated;  
    DateTime DateLastModified;  
    DateTime DatePosted;  
    DateTime DateRevised;  
    DateTime EffectiveDate;  
    UInt32 EULAAccepted;  
    Boolean EULAExists;  
    DateTime EULASignoffDate;  
    String EULASignoffUser;  
    UInt32 ExecutionContext;  
    Boolean IsBundle;  
    Boolean IsContentProvisioned;  
    Boolean IsDeployable;  
    Boolean IsDeployed;  
    Boolean IsDigest;  
    Boolean IsEnabled;  
    Boolean IsExpired;  
    Boolean IsHidden;   
    Boolean IsLatest;  
    Boolean IsMetadataOnlyUpdate;  
    Boolean IsOfflineServiceable;  
    Boolean IsQuarantined;  
    Boolean IsSuperseded;  
    Boolean IsUserDefined;  
    String LastModifiedBy;  
    DateTime LastStatusTime;  
    String LocalizedCategoryInstanceNames[];  
    String LocalizedDescription;  
    String LocalizedDisplayName;  
    SMS_CI_LocalizedEulas LocalizedEulas[];  
    SMS_CI_LocalizedProperties LocalizedInformation[];  
    String LocalizedInformativeURL;  
    UInt32 LocalizedPropertyLocaleID;   
    UInt32 MaxExecutionTime;  
    UInt32 ModelID;  
    String ModelName;   
    UInt32 NumMissing;  
    UInt32 NumNotApplicable;  
    UInt32 NumPresent;  
    UInt32 NumTotal;  
    UInt32 NumUnknown;  
    UInt32 PercentCompliant;  
    UInt32 PermittedUses;   
    String PlatformCategoryInstance_UniqueIDs[];  
    UInt32 PlatformType;  
    Boolean RequiresExclusiveHandling;  
    UInt32 RevisionNumber;  
    SMS_SDMPackageLocalizedData SDMPackageLocalizedData[];  
    UInt32 SDMPackageVersion;  
    String SDMPackageXML;   
    String SecuredScopeNames[];  
    String SedoObjectVersion;  
    UInt32 Severity;  
    String SeverityName;  
    SInt64 Size;  
    String SourceSite;  
    String UpdateLocales[];  
};  

```  

## Methods  
 The `SMS_ServicePlan` class does not define any methods.  

## Properties  
 `ApplicabilityCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("512"), not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `ArticleID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read, SizeLimit("64"), not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `BulletinID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers:  [read, SizeLimit("64"), not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CategoryInstance_UniqueIDs`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CIType_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read, enumeration]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `ConfigurationFlags`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [bits("COMPLIANCE_POLICY(0)"), read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"),read, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CustomSeverity`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `CustomSeverityName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `DateLastModified`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `DatePosted`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers:  [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `DateRevised`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `EffectiveDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `EULAAccepted`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `EULAExists`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `EULASignoffDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `EULASignoffUser`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `ExecutionContext`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, valuemap, values]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsBundle`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsContentProvisioned`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsDeployable`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers:  [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsDeployed`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsDigest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsExpired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsHidden`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsLatest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsMetadataOnlyUpdate`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers:  [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsOfflineServiceable`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsQuarantined`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsSuperseded`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `IsUserDefined`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"), read, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LastStatusTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers:  [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LocalizedDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LocalizedEulas[]`  
 Data type: `SMS_CI_LocalizedEulas`  

 Access type: [read,lazy]  

 Qualifiers: none  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LocalizedInformation[]`  
 Data type: `SMS_CI_LocalizedProperties`  

 Access type: [read, lazy]  

 Qualifiers: none  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LocalizedInformativeURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `MaxExecutionTime`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `ModelID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `NumMissing`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `NumNotApplicable`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `NumPresent`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `NumTotal`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `NumUnknown`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `PercentCompliant`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `PermittedUses`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `PlatformCategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `PlatformType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bitmap, bitvalues, read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `RequiresExclusiveHandling`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `RevisionNumber`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `SDMPackageLocalizedData`  
 Data type: `SMS_SDMPackageLocalizedData` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `SDMPackageXML`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `SecuredScopeNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `Severity`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `SeverityName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `Size`  
 Data type: `sint64`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

 `UpdateLocales`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SoftwareUpdateBase Server WMI Class](../../../develop/reference/sum/sms_softwareupdatebase-server-wmi-class.md).  

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
 [Configuration Manager Software Updates Server WMI Classes](../../../develop/reference/sum/software-updates-server-wmi-classes.md)
