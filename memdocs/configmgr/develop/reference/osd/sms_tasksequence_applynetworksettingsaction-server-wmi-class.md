---
title: "SMS_TaskSequence_ApplyNetworkSettingsAction Class"
titleSuffix: "Configuration Manager"
description: "Represent a task sequence action that specifies the network or workgroup configuration information for the target computer."  
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 58711e92-36da-48f3-affe-9d095a45b1cc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_TaskSequence_ApplyNetworkSettingsAction Server WMI Class
The `SMS_TaskSequence_ApplyNetworkSettingsAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that specifies the network or workgroup configuration information for the target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ApplyNetworkSettingsAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_NetworkAdapterSettings Adapters[];  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      String DNSDomain;  
      String DNSSuffixSearchOrder[];  
      String DomainName;  
      String DomainOUName;  
      String DomainPassword;  
      String DomainUsername;  
      Boolean Enabled;  
      Boolean EnableTCPIPFiltering;  
      String Name;  
      UInt32 NetworkJoinType;  
      UInt32 NumAdapters;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      String WorkgroupName;  
};  
```  

## Methods  
 The `SMS_TaskSequence_ApplyNetworkSettingsAction` class does not define any methods.  

## Properties  
 `Adapters`  
 Data type: `SMS_TaskSequence_NetworkAdapterSettings` Array  

 Access type: Read/Write  

 Qualifiers: [Global, VariableName("OSDAdapter")]  

 [SMS_TaskSequence_NetworkAdapterSettings Server WMI Class](../../../develop/reference/osd/sms_tasksequence_networkadaptersettings-server-wmi-class.md) objects representing settings for the adapters installed on the target computer. This property must be global so that it is visible in finalize mode.  

 The task sequence variable associated with this property is OSDAdapter. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDAdapter).  

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

 `DNSDomain`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Global]  

 The primary Domain Name System (DNS) domain. This property must be global so that it is visible in finalize mode.  

 `DNSSuffixSearchOrder`  
 Data type: `String` Array  

 Access type: Read/Write  

 Qualifiers: [Global]  

 The DNS suffix search order. This property must be global so that it is visible in finalize mode.  

 `DomainName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNull("WorkgroupName"), AllowedLen("1-255")]  

 Name of the domain for the target computer. The name can be between 1 and 255 characters in length. Supply this name if `NetworkJoinType` is set to 0.  

 `DomainOUName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-32767")]  

 The name of the Active Directory organizational unit (OU) to which the user belongs. The name can be between 0 and 32,767 characters in length. Set this property if `NetworkJoinType` is set to 0.  

 `DomainPassword`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDJoinPassword"), Secret]  

 Password of the account used when the user joins a Windows domain. Set this property if `NetworkJoinType` is set to 0.  

 The task sequence variable associated with this property is OSDJoinPassword. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDJoinPassword).  

 `DomainUsername`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("OSDJoinAccount")]  

 Account used when the user joins a Windows domain. Set this property if `NetworkJoinType` is set to 0.  

 The task sequence variable associated with this property is OSDJoinAccount, which specifies the network account that should be used to add the target computer to a Windows domain. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDJoinAccount).  

 `Enabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `EnableTCPIPFiltering`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [Global]  

 `true` to enable TCP/IP filtering. The default value is `false`. This property must be global so that it is visible in finalize mode.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("1-100")]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `NetworkJoinType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 The type of network join supported by the target computer. Possible values are:  

| Value | Network join type |  
| ----- | ----------------- |  
|0|Domain|  
|1|Workgroup|  

 `NumAdapters`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [Global, VariableName("OSDAdapterCount")]  

 Size of the array indicated by the `Adapters` property. This property must be global so that it is visible in finalize mode.  

 The task sequence variable associated with this property is OSDAdapterCount. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md#OSDAdapterCount).  

 OSDAdapterCount  

 `SupportedEnvironment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null:ToInstance]  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `Timeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 `WorkgroupName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [RequiredIfNull("DomainName"), AllowedLen("1-32")]  

 Name of the workgroup joined by the target computer. The name can be between 1 and 32 characters in length. Set this property if `NetworkJoinType` is set to 1.  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("osdnetsettings.exe configure"),VariablePrefix("OSD"), ActionCategory{"Settings,3,7"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "ApplyNetworkSettingsControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  
