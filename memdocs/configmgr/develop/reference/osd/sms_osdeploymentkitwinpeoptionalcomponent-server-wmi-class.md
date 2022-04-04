---
title: "SMS_OSDeploymentKitWinPEOptionalComponent Class"
titleSuffix: "Configuration Manager"
description: "In Configuration Manager, the SMS_OSDeploymentKitWinPEOptionalComponent WMI class is an SMS Provider server class that Maps Assessment and Deployment Kit versions to supported optional components."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 972bf59c-9d64-49ff-bd5d-77c7fed7eb36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_OSDeploymentKitWinPEOptionalComponent Server WMI Class
The `SMS_OSDeploymentKitWinPEOptionalComponent` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that Maps Assessment and Deployment Kit (ADK) versions to supported optional components.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_OSDeploymentKitWinPEOptionalComponent : SMS_WinPEOptionalComponentInfo  
{  
    String Architecture;  
    String DependentComponentNames[];  
    UInt32 DependentIds[];  
    String DeploymentKitVersion;  
    Boolean IsRequired;  
    UInt32 LanguageID;  
    String Name;  
    String RelativePath;  
    UInt64 Size;  
    UInt32 UniqueID;  
};  

```  

## Methods  
 The `SMS_OSDeploymentKitWinPEOptionalComponent`  class does not define any methods.  

## Properties  
 `Architecture`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

 `DependentComponentNames`  
 Data type: `String Array`  

 Access type: Read  

 Qualifiers: none  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

 `DependentIds`  
 Data type: `UInt32 Array`  

 Access type: Read  

 Qualifiers: none  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md)>.  

 `DeploymentKitVersion`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [not_null]  

 The version of the deployment kit with which this property is associated.  

 `IsRequired`  
 Data type: `Boolean`  

 Access type: Read  

 Qualifiers: none  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

 `LanguageID`  
 Data type: `Unit32`  

 Access type: Read  

 Qualifiers: [key]  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

 `RelativePath`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: none  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

 `Size`  
 Data type: `UInt34`  

 Access type: Read  

 Qualifiers: none  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

 `UniqueID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers: [key]  

 See [SMS_WinPEOptionalComponentInfo Server WMI Class](../../../develop/reference/osd/sms_winpeoptionalcomponentinfo-server-wmi-class.md).  

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
