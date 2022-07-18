---
title: "SMS_MDMAppleVppLicense Class"
titleSuffix: "Configuration Manager"
description: "The SMS_MDMAppleVppLicense WMI class represents an Apple Volume Purchase Program (VPP) licensed application."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4a368d69-28a1-49bc-9a50-fa184f2b07cc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_MDMAppleVppLicense Server WMI Class
The `SMS_MDMAppleVppLicense` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an Apple Volume Purchase Program (VPP) licensed application.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_MDMAppleVppLicense : SMS_BaseClass  
{  
    String ApplicationID;  
    UInt32 AvailableLicenses;  
    String BundleID;  
    String DeepLinkUrl;  
    String InfoLink;  
    DateTime LastUpdateTime;  
    String Publisher;  
    DateTime ReleaseDate;  
    String SupportedDevices;  
    String Title;  
    UInt32 TotalLicenses;  
    String Version;  
};  

```  

## Methods  
 The `SMS_MDMAppleVppLicense`  class does not define any methods.  

## Properties  
 `ApplicationID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key]  

 The AppleID of the application.  

 `AvailableLicenses`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Current number of available licenses for the application.  

 `BundleID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Apple App Store bundle ID.  

 `DeepLinkUrl`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The application VPP link in the Apple App Store.  

 `InfoLink`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The link to the application in the Apple App Store.  

 `LastUpdateTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The last time the VPP license data for the application was updated.  

 `Publisher`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Publisher of the application in the Apple App Store.  

 `ReleaseDate`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: none  

 The application's release date to the Apple App Store.  

 `SupportedDevices`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 The devices supported by the application.  

 `Title`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Title of the application in Apple App Store.  

 `TotalLicenses`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Total number of licenses for the application.  

 `Version`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Application version in the Apple App Store.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Secured  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
