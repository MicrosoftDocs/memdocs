---
title: "SMS_CM_UpdateFeatures Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9de78bee-635b-470e-a090-37c097fbad7dsearchScope: - ConfigMgr SDK
caps.latest.revision: 4
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_CM_UpdateFeatures Server WMI Class
The  `SMS_CM_UpdateFeatures` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents update feature extensions.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_CM_UpdateFeatures : SMS_BaseClass  
{  
    DateTime DateReleased;  
    String Description;  
    String EULA;  
    UInt32 Exposed;  
    String FeatureGuid  
    SInt32 FeatureType;  
    SInt32 LocaleID;  
    String MoreInfoLink;  
    String Name;  
    SInt32 Status;  
};  

```  

## Methods  
 The following table lists the methods in the `SMS_CM_UpdateFeatures` class.  

|Method|Description|  
|------------|-----------------|  
|[UpdateFeatureExposureStatus Method in Class SMS_CM_UpdateFeatures](../../../develop/reference/sum/updatefeatureexposurestatus-method-in-class-sms_cm_updatefeatures.md)|Updates the feature exposure status for an update feature extension.|  

## Properties  
 `DateReleased`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: none  

 The release date of the package, including the feature.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Description for the feature extension.  

 `EULA`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Microsoft Software License Terms for the feature extension.  

 `Exposed`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Bit value for exposing a feature.  

 `FeatureGuid`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 A unique identifier for a feature.  

 `FeatureType`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Flag indicating the latest type of the feature. The default value is 1.  

 `LocaleID`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 The locale ID for the localized data.  

 `MoreInfoLink`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Link to additional information about the feature extension.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the feature extension.  

 `Status`  
 Data type: `SInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Flag indicating whether a feature will be exposed.  

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
