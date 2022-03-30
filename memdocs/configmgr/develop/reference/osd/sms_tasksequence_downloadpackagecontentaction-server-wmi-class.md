---
title: "SMS_TaskSequence_DownloadPackageContentAction Class"
titleSuffix: "Configuration Manager"
description: "Represents a task sequence action that downloads the contents of a package."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 59c5be42-51d9-45dc-a896-ad177a58f9b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_DownloadPackageContentAction Server WMI Class
The `SMS_TaskSequence_DownloadPackageContentAction` Windows Management Instrumentation (WMI) class is an SMS provider server class, in Configuration Manager, that represents a task sequence action that downloads the contents of a package.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_DownloadPackageContentAction : SMS_TaskSequence_Action  
{  
    SMS_TaskSequence_Condition Condition;  
    Boolean ContinueDownloadOnError;  
    Boolean ContinueOnError;  
    String Description;  
    String DestinationCustomPath;  
    String DestinationLocationType;  
    String DestinationVariable;  
    String DownloadPackages;  
    Boolean Enabled;  
    String Name;  
    UInt32 NumPackages;  
    SMS_TaskSequence_PackageInfo PackageInfo[];  
    String SupportedEnvironment;  
    UInt32 Timeout;  
};  

```  

## Methods  
 The `SMS_TaskSequence_DownloadPackageContentAction` class does not define any methods.  

## Properties  
 `Condition`  
 Data type:  `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `ContinueDownloadOnError`  
 Data type:   `Boolean`  

 Access type: Read/Write  

 Qualifiers: none  

 `true` to continue to the next package if a package fails to download.  The default value is `true`.  

 `ContinueOnError`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-255")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `DestinationCustomPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:   [VariableName("OSDDownloadDestinationPath")]  

 The destination path.  

 `DestinationLocationType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:  [Not_Null, ValueMap]  

 The destination location type. The default value is TSCache. Possible values are:  

|Value|
|-|  
|TSCache|  
|CCMCache|  
|Custom|  

 `DestinationVariable`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The destination variable.  

 `DownloadPackages`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, TaskSequencePackageList]  

 Comma separated list of package Ids to be downloaded.  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `NumPackages`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDPackageCount")]  

 The total number of packages.  

 `PackageInfo`  
 Data type:   `SMS_TaskSequence_PackageInfo Array`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDPackage")]  

 An array of task sequence information package information.  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The default value is WinPEandFullOS. See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
