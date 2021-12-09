---
title: "SMS_ConfigurationItem Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 527389f5-99e3-4978-a807-4e5e3c5acc04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_ConfigurationItem Server WMI Class
The `SMS_ConfigurationItem` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a configuration item.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ConfigurationItem : SMS_ConfigurationItemBaseClass  
{  
      String ApplicabilityCondition;  
      String CategoryInstance_UniqueIDs;[]  
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
      Boolean InUse;  
      Boolean IsBroken;  
      Boolean IsBundle;  
      Boolean IsChild;   
      Boolean IsDigest;  
      Boolean IsEnabled;  
      Boolean IsExpired;  
      Boolean IsHidden;  
      Boolean IsLatest;  
      Boolean IsQuarantined;  
      Boolean IsSuperseded;  
      Boolean IsUserDefined;  
      String LastModifiedBy;  
      String LocalizedCategoryInstanceNames;[]  
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
 The following table lists the methods in the `SMS_ConfigurationItem` class.  

|Method|Description|  
|------------|-----------------|  
|[AcceptEULA Method in Class SMS_ConfigurationItem](../../../develop/reference/compliance/accepteula-method-in-class-sms_configurationitem.md)|Accepts or declines the Microsoft Software License Terms of a configuration item.|  
|[GetEULA Method in Class SMS_ConfigurationItem](../../../develop/reference/compliance/geteula-method-in-class-sms_configurationitem.md)|Gets the localized Microsoft Software License Terms content of the configuration item.|  
|[GetSDMDefinition Method in Class SMS_ConfigurationItem](../../../develop/reference/compliance/getsdmdefinition-method-in-class-sms_configurationitem.md)|Retrieves the System Definition Model (SDM) definition of the configuration item in XML format.|  
|[SetEnforcement Method in Class SMS_ConfigurationItem](../../../develop/reference/compliance/setenforcement-method-in-class-sms_configurationitem.md)|Sets the enforcement and the enforcement date for a configuration item.|  

## Properties  
 `ApplicabilityCondition`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("512"), not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CategoryInstance_UniqueIDs`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CI_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CI_UniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers:[unique, not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CIType_ID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 For this class, the type ID is OtherConfigurationItem (7).  

 `CIVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `ConfigurationFlags`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `CreatedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"), read, not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `DateCreated`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read, not_null]  

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

 `InUse`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 [SMS_ConfigurationBaselineInfo Server WMI Class](../../../develop/reference/compliance/sms_configurationbaselineinfo-server-wmi-class.md)  

 `IsBroken`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if the configuration item is broken.  

 `IsBundle`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsChild`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read]  

 `true` if this configuration item is a child of other configuration item.  

 `IsDigest`  
 Data type: `Boolean`  

 Access type: Read-only  

 Qualifiers: [read, lazy]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsEnabled`  
 Data type: `Boolean`  

 Access type: `Read/Write`  

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

 Qualifiers: [read, not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `IsUserDefined`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LastModifiedBy`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [SizeLimit("512"), read, not_null]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String` Array  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedDescription`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedEulas`  
 Data type: `SMS_CI_LocalizedEulas Array`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 An array of localized Microsoft Software License Terms for the configuration item.  

 `LocalizedDisplayName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

 `LocalizedInformation`  
 Data type: `SMS_CI_LocalizedProperties` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A list of language-specific localized information about the configuration item:  

- `String` DisplayName  

- `String` Description  

- `String` InformativeURL  

- `UInt32` LocaleID  

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

  Access type: Read-only  

  Qualifiers: [unique, not_null]  

  See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

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

  `SDMPackageLocalizedData`  
  Data type: `SMS_SDMPackageLocalizedData` Array  

  Access type: Read/Write  

  Qualifiers: [lazy]  

  See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

  `SDMPackageVersion`  
  Data type: `UInt32`  

  Access type: Read-only  

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

  `SourceSite`  
  Data type: `String`  

  Access type: Read-only  

  Qualifiers: [SizeLimit("3")]  

  See [SMS_ConfigurationItemLatestBaseClass Server WMI Class](../../../develop/reference/compliance/sms_configurationitemlatestbaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

  Your application uses this class by creating an object and getting and setting the properties as required for the particular configuration.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Compliance Settings (DCM) Server WMI Classes](../../../develop/reference/compliance/compliance-settings-dcm-server-wmi-classes.md)
