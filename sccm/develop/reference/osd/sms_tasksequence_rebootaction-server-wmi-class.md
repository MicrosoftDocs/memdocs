---
title: "SMS_TaskSequence_RebootAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 718afd29-a3cc-436a-9cb7-7e35e0e77f59
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TaskSequence_RebootAction Server WMI Class
The `SMS_TaskSequence_RebootAction` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence action that specifies restart options for the target computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequence_RebootAction : SMS_TaskSequence_Action  
{  
      SMS_TaskSequence_Condition Condition;  
      Boolean ContinueOnError;  
      String Description;  
      Boolean Enabled;  
      String Message;  
      UInt32 MessageTimeout;  
      String Name;  
      String SupportedEnvironment;  
      String Target;  
      UInt32 Timeout;  
};  
```  

## Methods  
 The `SMS_TaskSequence_RebootAction` class does not define any methods.  

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

 `Message`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [AllowedLen("0-512")]  

 A user-defined message for display in the reboot dialog box. The message length can be between 0 and 512 characters.  

 `MessageTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [VariableName("SMSRebootTimeout")]  

 The number of seconds that a user-defined message is displayed to the user before the computer restarts. Specify 0 seconds (default) to indicate that no reboot message should be displayed.  

 The task sequence variable that is associated with this property is SMSRebootTimeout. For more information, see the MSDN documentation for [Operating System Deployment Task Sequence Variables](http://go.microsoft.com/fwlink/?LinkId=100711).  

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

 `Target`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [Not_Null, CommandLineArg(1)]  

 The operating system to use for reboot. Possible values are:  

- HD  

- WinPE  

  `Timeout`  
  Data type: `UInt32`  

  Access type: Read/Write  

  Qualifiers: None  

  See [SMS_TaskSequence_Action Server WMI Class](../../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

 [CommandLine("smsboot.exe /target:%1"),VariablePrefix("SMSReboot"),  

 ActionCategory("General,6,1"),ActionUI{"AdminUI.TaskSequenceEditor.dll", "Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor", "RebootComputerControl", "TaskSequenceOptionControl"}]  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)
