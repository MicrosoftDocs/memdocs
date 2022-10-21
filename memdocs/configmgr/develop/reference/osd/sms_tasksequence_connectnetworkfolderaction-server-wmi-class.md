---
description: Learn how to represent a task sequence action that makes a connection to a network share with SMS_TaskSequence_ConnectNetworkFolderAction.
title: SMS_TaskSequence_ConnectNetworkFolderAction Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 3d4a32d4-7a09-41dc-8e94-0d087ade9f94
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS_TaskSequence_ConnectNetworkFolderAction Server WMI Class
The `SMS_TaskSequence_ConnectNetworkFolderAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that makes a connection to a network share.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_ConnectNetworkFolderAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      String DriveLetter;  
      Boolean Enabled;  
      String Name;  
      String Password;  
      String Path;  
      String SupportedEnvironment;  
      UInt32 Timeout;  
      String Username;  
};  
```  

## Methods  
 The `SMS_TaskSequence_ConnectNetworkFolderAction` class does not define any methods.  

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

 `DriveLetter`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Drive letter to use for connection to the network share.  

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

 `Password`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("SMSConnectNetworkFolderPassword"), Not_Null, Secret]  

 Password to use to connect to the network share.  

 The task sequence variable associated with this property is SMSConnectNetworkFolderPassword. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

 `Path`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null]  

 The path to which to connect.  

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

 `Username`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [VariableName("SMSConnectNetworkFolderAccount"), Not_Null]  

 Account that should be used to connect to the network share.  

 The task sequence variable associated with this property is SMSConnectNetworkFolderAccount. For more information, see [OS deployment task sequence variables](../../../osd/understand/task-sequence-variables.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("smsnetuse.exe %SMSConnectNetworkFolderPath%"),  

 VariablePrefix("SMSConnectNetworkFolder"),  

 ActionCategory{"General,5,1"},ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "ConnectNetworkFolderControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See also

[SMS_TaskSequence_Action server WMI class](sms_tasksequence_action-server-wmi-class.md)
