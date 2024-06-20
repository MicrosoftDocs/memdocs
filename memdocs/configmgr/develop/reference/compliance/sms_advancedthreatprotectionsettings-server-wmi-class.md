---
title: SMS_AdvancedThreatProtectionSettings Class
titleSuffix: Configuration Manager
ms.date: 05/13/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 276d3f64-bd9b-4112-b869-bdad7d8b6931
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
description: An overview of SMS_AdvancedThreatProtectionSettings Server WMI Class
ms.reviewer: mstewart,aaroncz 
---
# SMS_AdvancedThreatProtectionSettings Server WMI Class
The  `SMS_AdvancedThreatProtectionSettings` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents policy settings for Microsoft Defender for Endpoint. 

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AdvancedThreatProtectionSettings : SMS_SettingsDefinitionBase  
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
 The `SMS_AdvancedThreatProtectionSettings` class does not define any methods.  

## Properties  
 `ApplicabilityCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("512"), not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `CategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:[unique, not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `CIType_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `ConfigurationFlags`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [bits("COMPLIANCE_POLICY(0)"), read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"),read, not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `DateLastModified`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `EffectiveDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `EULAAccepted`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `EULAExists`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `EULASignoffDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `EULASignoffUser`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `ExecutionContext`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, valuemap, values]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `InUse`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsBroken`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsBundle`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsDigest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsExpired`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsHidden`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsLatest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsQuarantined`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsSuperseded`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `IsUserDefined`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"), read, not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LocalizedDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LocalizedEulas`  
 Data type: `SMS_CI_LocalizedEulas Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LocalizedInformation`  
 Data type: `SMS_CI_LocalizedProperties Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LocalizedInformativeURL`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `LocalizedPropertyLocaleID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `ModelID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `ModelName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [unique,not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `PermittedUses`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `PlatformCategoryInstance_UniqueIDs`  
 Data type: `String Array`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `PlatformType`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bitmap, bitvalues, read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `SDMPackageLocalizedData`  
 Data type: `SMS_SDMPackageLocalizedData Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `SDMPackageVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `SDMPackageXML`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `SecuredScopeNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("3")]  

 See [SMS_SettingsDefinitionBase Server WMI Class](../../../develop/reference/compliance/sms_settingsdefinitionbase-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
