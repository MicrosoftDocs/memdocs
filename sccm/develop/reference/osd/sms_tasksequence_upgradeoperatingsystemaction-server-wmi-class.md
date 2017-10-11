---
title: "SMS_TaskSequence_UpgradeOperatingSystemAction Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "12/01/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4a5f6ade-6ab5-4324-ac0e-6348b9488712searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_UpgradeOperatingSystemAction Server WMI Class
The `SMS_TaskSequence_UpgradeOperatingSystemAction` Windows Management Instrumentation (WMI) class is an SMS provider server class, in Configuration Manager, that represents a task sequence action that upgrades the operating system. This is only supported for Windows 10 and Windows 10 Anniversary Update.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_UpgradeOperatingSystemAction : SMS_TaskSequence_Action  
{  
    SMS_TaskSequence_Condition Condition;  
    Boolean ContinueOnError;  
    String Description;  
    String DriverPackageID;  
    String DynamicUpdateSettings;  
    Boolean Enabled;  
    Boolean IgnoreMessages;  
    UInt32 InstallEditionIndex;  
    String InstallPackageID;  
    String InstallPath;  
    String Name;  
    String OsProductKey;  
    String PreserveSettings;  
    UInt32 SetupTimeout;  
    String SupportedEnvironment;  
    UInt32 Timeout;  
};  

```  

## Methods  
 The `SMS_TaskSequence_UpgradeOperatingSystemAction` class does not define any methods.  

## Properties  
 `Condition`  
 Data type: `SMS_TaskSequence_Condition`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

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

 `DriverPackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [TaskSequencePackage]  

 The package ID of the driver package to use during upgrade.  

 `DynamicUpdateSettings`  
 Data type: `string`  

 Access type: Read/Write  

 Qualifiers:  [ValueMap]  

 Specifies whether to dynamically update Windows Setup with Windows Update.  

|Possible values|  
|----|  
|Disable|  
|OveridePolicy|  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `IgnoreMessages`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 Ignores dismissible compatibility messages. The default value is `false`.  

 `InstallEditionIndex`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The installation edition index. The default value is 1.  

 `InstallPackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [TaskSequencePackage("image"), RequiredIfNull("InstallPath")]  

 The ID of the operating system installation package to use for  upgrades.  

 `InstallPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNull("InstallPackageID")]  

 The path or environment variable to the operating system installation package to use for the upgrade.  

 `Name`  
 Data type:  `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `OsProductKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [QuasiSecret]  

 The product key for the operating system upgrade content.  

 `PreserveSettings`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers:  [ValueMap]  

 Specifies what data to keep during an upgrade. The default value is Upgrade, which keeps applications, data, and settings. For best results, use the default value.  

 `ScanOnly`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 Performs a Windows Setup compatibility scan without starting the upgrade. The default value is `false`.  

 `SetupTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The timeout that applies when running Windows Setup from the command line during an upgrade.  

 `StagedContent`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The path or environment variable to the driver content to use for the upgrade.  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The default value is FullOS. See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
