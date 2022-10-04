---
title: SMS_TaskSequence_CaptureNetworkSettingsAction class
titleSuffix: Configuration Manager
description: Details of the SMS_TaskSequence_CaptureNetworkSettingsAction server WMI class
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 7180bd80-e003-4258-b21f-bf4d6964ac9f
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# SMS_TaskSequence_CaptureNetworkSettingsAction server WMI class

The `SMS_TaskSequence_CaptureNetworkSettingsAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that captures network settings from the target computer.

The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_CaptureNetworkSettingsAction : SMS_TaskSequence_Action  
{  
          SMS_TaskSequence_Condition Condition;  
          Boolean ContinueOnError;  
          String Description;  
          Boolean Enabled;  
          Boolean MigrateAdapterSettings;  
          Boolean MigrateNetworkMembership;  
          String Name;  
          String SupportedEnvironment;  
          UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_CaptureNetworkSettingsAction` class does not define any methods.  

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

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `MigrateAdapterSettings`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDMigrateAdapterSettings")]  

 `true` (default) to migrate TCP/IP and DNS settings for network adapters.  

 The task sequence variable associated with this property is OSDMigrateAdapterSettings. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDMigrateAdapterSettings).  

 `MigrateNetworkMembership`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null, VariableName("OSDMigrateNetworkMembership")]  

 `true` to migrate workgroup or domain membership information as part of operating system deployment. The default value is `false`.  

 The task sequence variable associated with this property is OSDMigrateNetworkMembership. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDMigrateNetworkMembership).  

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

 The default value of this property for this task sequence action is FullOS.  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdnetsettings.exe capture netmembership:%%OSDMigrateNetworkMembership%% adapters:%%OSDMigrateAdapterSettings%%"),  

 ActionCategory{"Settings,1,7"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "CaptureNetworkSettingsControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md)
