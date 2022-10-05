---
title: SMS_CM_UpdatePackageFeatures Class
description: Learn how to use the SMS_CM_UpdatePackageFeatures class in Configuration Manager to update feature extensions.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 1f1b0614-be4e-4e4a-a2a5-6df5a2d97c1c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_CM_UpdatePackageFeatures Server WMI Class
The  `SMS_CM_UpdatePackageFeatures` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents update feature extensions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_UpdatePackageFeatures : SMS_BaseClass  
{  
    String Description;  
    String EULA;     
    UInt32 Exposed;  
    String FeatureGuid;  
    SInt32 FeatureType;  
    SInt32 Flag;   
    SInt32 LocaleID;  
    String MoreInfoLink;  
    String Name;  
    String PackageGuid;  
    SInt32 Status;  
 };  

```  

## Methods  
 The following table lists the methods in the `SMS_CM_UpdatePackageFeatures` class.  

|Method|Description|  
|------------|-----------------|  
|[UpdateFeatureExposureStatus Method in Class SMS_CM_UpdatePackageFeatures](../../../develop/reference/sum/updatefeatureexposurestatus-method-in-class-sms_cm_updatepackagefeatures.md)|Updates the feature exposure status for an update package feature extension.|  

## Properties  
 `Description`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Description for the feature extension.  

 `EULA`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [lazy]  

 Microsoft Software License Terms for the feature extension.  

 `Exposed`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: none  

 Bit value for exposing a feature.  

 `FeatureGuid`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 A unique identifier for a feature.  

 `FeatureType`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 Type of the feature in the package.  

 `Flag`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 Flag indicating the latest type of the feature.  

 `LocaleID`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 The locale ID for the localized data.  

 `MoreInfoLink`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Link to additional information about the feature extension.  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 Name of the feature extension.  

 `PackageGuid`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [key, not_null]  

 A unique identifier for the feature.  

 `Status`  
 Data type: `SInt32`  

 Access type: Read  

 Qualifiers: none  

 Flag indicating whether a feature will be exposed.  

## Remarks  
 Class qualifiers for this class include:  

- Dynamic  

- Read (read-only)  

  For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
