---
title: "SMS_TaskSequence_AutoApplyAction Class"
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
ms.assetid: f330dd6f-9453-4fe2-b285-a7287c0853d0searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequence_AutoApplyAction Server WMI Class
The `SMS_TaskSequence_AutoApplyAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that matches and installs device drivers as part of an operating system deployment.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_AutoApplyAction : SMS_TaskSequence_Action  
{  
      Boolean BestMatch;  
      String CategoryList[];  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String Name;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      Boolean UnsignedDriver;  
};  
```  

## Methods  
 The `SMS_TaskSequence_AutoApplyAction` class does not define any methods.  

## Properties  
 `BestMatch`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 `true` (default) to install the device driver that is the best match for the hardware device. Set this property to `false` to install all compatible device drivers and have the operating system choose the best driver to use.  

> [!NOTE]
>  This property is required by the task sequence action if there are multiple device drivers in the driver catalog that are compatible with the hardware device.  

 `CategoryList`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: None  

 Unique IDs of categories for which the task sequence action searches in the driver catalog. The default value is `null`.  

 You can obtain the available category IDs by enumerating the SMS_CategoryInstance Server WMI Class objects on the site.  

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

 The default value of this property for this task sequence action is WinPE.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `UnsignedDriver`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, VariableName("OSDAllowUnsignedDriver")]  

 `true` to configure the Windows operating system to allow unsigned device drivers to be installed. The default value is `false`.  

 The task sequence variable associated with this property is OSDAllowUnsignedDriver. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

> [!NOTE]
>  This property is required by the task sequence action. Unattended installation of unsigned drivers is done on versions of Windows where this is allowed.  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osddriverclient.exe /auto /bestmatch:%%OSDAutoApplyDriverBestMatch%% /unsigned:%%OSDAllowUnsignedDriver%%"),  

 ActionCategory{"Drivers,1,6"},VariablePrefix("OSDAutoApplyDriver"),  

 ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "AutoApplyDriverControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)
