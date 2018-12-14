---
title: "SMS_LicensedVppApps Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c5c499ab-97f4-4d11-befa-e5151db75cba
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_LicensedVppApps Server WMI Class
The `SMS_LicensedVppApps` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents license Information for Apple App Store Volume Purchase Program (VPP) and Microsoft Store for Business applications.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_LicensedVppApps : SMS_BaseClass  
{  
    String ApproximateSize;  
    String ApplicationID;  
    String ApplicationMetadata;  
    SInt32 AvailableLicenses;  
    DateTime ContentLastModified;  
    DateTime CreatedDate;         
    String DisplayName;  
    DateTime LastSuccessfulSync;  
    DateTime LastSync;  
    UInt32 LicenseType;     
    UInt32 Platform;  
    String Publisher;  
    String SoftwareVersion;  
    String StoreCategory;  
    String StoreLink;  
    String SupportedLanguages;  
    String SupportedProcessors;  
    SInt32 TotalLicenses;  
};  

```  

## Methods  
 The `SMS_LicensedVppApps` class does not define any methods.  

## Properties  
 `ApproximateSize`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The approximate size of the application.  

 `ApplicationID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The ID of the application.  

 `ApplicationMetadata`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [lazy]  

 The application metadata.  

 `AvailableLicenses`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 The number of available licenses for the application.  

 `ContentLastModified`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The date and time that the content was last modified.  

 `CreatedDate`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The date the application was created.  

 `DisplayName`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The display name of the application.  

 `LastSuccessfulSync`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The date and time of the last successful synchronization.  

 `LastSync`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The date and time of the last synchronization.  

 `LicenseType`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 The type of license. Possible values are:  

|||  
|-|-|  
|0|Online|  
|1|Offline|  

 `Platform`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 The platform on which the application runs. Possible values are:  

|||  
|-|-|  
|0 or 1|Windows|  
|2|iOS|  

 `Publisher`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The name of the publisher of the application.  

 `SoftwareVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The application version.  

 `StoreCategory`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The category of the application in the store.  

 `StoreLink`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The link to the application in the store.  

 `SupportedLanguages`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The languages the application supports.  

 `SupportedProcessors`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The processor architectures that the application supports.  

 `TotalLicenses`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 The total number of licenses for the application. -1 indicates unlimited licenses.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

- Secured  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
