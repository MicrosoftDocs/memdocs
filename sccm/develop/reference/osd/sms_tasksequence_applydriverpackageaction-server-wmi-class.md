---
title: "SMS_TaskSequence_ApplyDriverPackageAction Class"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: a84ea8fa-ba47-4e73-a946-9eb579feadd6searchScope: - ConfigMgr SDK
caps.latest.revision: 16
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_ApplyDriverPackageAction Server WMI Class
The `SMS_TaskSequence_ApplyDriverPackageAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an action used in a task sequence to make all device drivers in a driver package available for use by Windows setup.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ApplyDriverPackageAction : SMS_TaskSequence_Action  
{  
        String BootCriticalContentUniqueID;  
        String BootCriticalDriverID;  
        String BootCriticalHardwareComponent;  
        String BootCriticalID;  
        String BootCriticalINFFile;  
        SMS_TaskSequence_Condition Condition;  
        Boolean ContinueOnError;  
        String Description;  
        String DriverPackageID;  
        Boolean Enabled;  
        String Name;  
        String SupportedEnvironment;  
        UInt32 Timeout;  
        Boolean UnsignedDriver;  
};  
```  

## Methods  
 The `SMS_TaskSequence_ApplyDriverPackageAction` class does not define any methods.  

## Properties  
 `BootCriticalContentUniqueID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNotNull]  

 The unique ID of the content associated a boot-critical mass storage device driver. If this ID is not specified, no mass-storage device driver is installed. The driver content can be obtained from the [SMS_CIToContent Server WMI Class](../../../develop/reference/sum/sms_citocontent-server-wmi-class.md) where the `CI_ID` property matches the driver ID. The default value is `null`.  

> [!NOTE]
>  This property is required if `BootCriticalDriverID` is set.  

 `BootCriticalDriverID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [CommandLineArg(2)]  

 Optional ID specified by the `CI_UniqueID` property of the [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md) object to install for a boot-critical mass storage device driver. The default value is `null`.  

 `BootCriticalHardwareComponent`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNotNull]  

 Hardware component used if a boot-critical mass storage device driver is being installed. The default value is `null`.  

> [!NOTE]
>  This property is required if `BootCriticalDriverID` is set.  

 `BootCriticalID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNotNull]  

 The boot-critical ID of the mass-storage device driver to be installed. The default value is `null`. This ID is listed in the "scsi" section of the device driver Txtsetup.oem file.  

> [!NOTE]
>  This property is required if `BootCriticalDriverID` is set.  

 `BootCriticalINFFile`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNotNull]  

 The INF file of a boot-critical mass-storage device driver to be installed. The default value is `null`.  

> [!NOTE]
>  This property is required if `BootCriticalDriverID` is set.  

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

 Qualifiers: [CommandLineArg(1), TaskSequencePackage, Not_Null]  

 ID of the driver package to install. This value is indicated by the `PackageID` property of the specific [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) object.  

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

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 The default value for this class is WinPE.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `UnsignedDriver`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("OSDAllowUnsignedDriver")]  

 `true` to configure Windows to allow unsigned device drivers to be installed. The default value is `false`.  

> [!NOTE]
>  This property is required by the action. However it is not used when deploying the Windows Vista operating system.  

 The task sequence variable associated with this property is OSDAllowUnsignedDriver. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osddriverclient.exe /install:%1 \<?2:\\"/bootcritical:%%OSDApplyDriverBootCriticalContentUniqueID%%,%%OSDApplyDriverBootCriticalINFFile%%,%%OSDApplyDriverBootCriticalHardwareComponent%%,%%OSDApplyDriverBootCriticalID%%\\">/unsigned:%%OSDAllowUnsignedDriver%%"),ActionCategory{"Drivers,2,6"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "ApplyDriverPackageControl", "TaskSequenceOptionControl"}, VariablePrefix("OSDApplyDriver")]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)   
 [SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)   
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)
