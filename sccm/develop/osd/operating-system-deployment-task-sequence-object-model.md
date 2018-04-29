---
title: "OS Deployment Task Sequence Object Model"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4176f9e2-aa68-44e0-bf47-d3cac73ca737
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Operating System Deployment Task Sequence Object Model
In System Center Configuration Manager, operating system deployment task sequences are created and edited by using a Windows Management Instrumentation (WMI) class-based object model.  

> [!CAUTION]
>  Changing task sequences by updating the task sequence XML is not supported. You will only need the XML when exporting the task sequence to different site. The XML is stored in the [SMS_TaskSequencePackage Server WMI Class](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)`Sequence` property.  

## Task Sequence Packages  
 A task sequence is packaged in an instance of the [SMS_TaskSequencePackage Server WMI Class](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) class and there is a single package for each task sequence. The package is advertised to client computers by using an instance of the [SMS_Advertisement Server WMI Class](../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) class. To associate the task sequence package with the advertisement, you set the [SMS_Advertisement Server WMI Class](../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) PackageID property to the [SMS_TaskSequencePackage Server WMI Class](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) PackageID property.  

> [!NOTE]
>  [SMS_TaskSequencePackage Server WMI Class](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) derives from [SMS_Package Server WMI Class](../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) and can be used in the same way that packages are used. For more information, see [Software Distribution Packages](../../develop/core/servers/configure/software-distribution-packages.md).  

 For more information about creating a task sequence package, see [How to Create an Operating System Deployment Task Sequence Package](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-package.md).  

 For more information about creating advertisements, see [How to Create an Advertisement](../../develop/core/servers/configure/how-to-create-an-advertisement.md).  

## Task Sequences  
 To create and manage task sequences, Configuration Manager provides a number of WMI classes that represent a task sequence, task sequence steps (actions and groups) and step conditions.  

 The key WMI classes are:  

### SMS_TaskSequence  
 The [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) class represents an individual task sequence. You can either create new instances of [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md), or you can use the method [SMS_TaskSequencePackage.GetSequence](../../develop/reference/osd/getsequence-method-in-class-sms_tasksequencepackage.md) to populate an [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) with an existing task sequence.  

> [!NOTE]
>  If you create a new [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md), you must associate it with a [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md). Otherwise, Configuration Manager is not aware of its existence.  

 The class property SMS_TaskSequence.Steps is an array of [SMS_TaskSequence_Step](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) derived classes. These steps are processed sequentially when the task sequence is run.  

### SMS_TaskSequenceStep  
 The two types of steps, action and group, derive from the [SMS_TaskSequenceStep](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) class. The two types of steps are the [SMS_TaskSequence_Group](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) class for groups and the [SMS_TaskSequence_Action](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md) derived class for the Configuration Manager built-in, or custom, actions.  

 A step has a number of properties that you can set.  

|Property|Description|  
|--------------|-----------------|  
|Condition|A condition that must be met for the step to be processed. This in an instance of the [SMS_TaskSequence_Condition](../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md) class.|  
|ContinueOnError|If set to `true`, the task sequence will continue to the next step when an error occurs. Otherwise the task sequence will propagate the failure back to the parent. If the parent is a group, the parent group's ContinueOnError property is evaluated. If the parent is the task sequence root, the task sequence will fail.|  
|Enabled|If set to `true`, the step is processed. Otherwise, the step is not processed.|  

 The step also has a Name and Description property.  

> [!NOTE]
>  This documentation refers to steps when the procedure is applicable to both actions and groups. For example, [How to Remove a Step From an Operating System Deployment Group](../../develop/osd/how-to-remove-a-step-from-an-operating-system-deployment-group.md) is a task that is applicable to both action removal and group removal.  

#### SMS_TaskSequenceAction  
 Configuration Manager defines a number of built-in actions that are defined in classes derived from the [SMS_TaskSequence_Action](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md) class. For example, the action that allows you to specify a command line is the [SMS_TaskSequence_RunCommandLineAction](../../develop/reference/osd/sms_tasksequence_runcommandlineaction-server-wmi-class.md) class.  

> [!NOTE]
>  The built-in actions are named SMS_TaskSequence_`ActionName`Action where `ActionName` is the name of the built-in action. They are documented in [Operating System Deployment Server WMI Classes](../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md).  

 In addition to the properties that are inherited from [SMS_TaskSequenceStep](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md), a derived action inherits the following properties from the [SMS_TaskSequence_Action](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md) class that you can set:  

|Property|Description|  
|--------------|-----------------|  
|SupportedEnvironment|Specifies the operating environment that the action can be run in. Valid values are "WinPE", "FullOS", "WinPEandFullOS.|  
|Timeout|Specifies the time-out period for the action, in seconds.|  

#### SMS_TaskSequenceGroup  
 The [SMS_TaskSequence_Group Server WMI Class](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) class represents a set of steps that are processed sequentially. [SMS_TaskSequence_Group Server WMI Class](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) Steps property is an array of [SMS_TaskSequence_Step Server WMI Class](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) classes that represent the group's steps. Because a group step is derived from [SMS_TaskSequence_Step Server WMI Class](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md), there can be further child groups within the steps.  

### SMS_TaskSequence_Condition  
 Each [SMS_TaskSequence_Step Server WMI Class](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) and the derived classes (actions and groups) can have an associated condition that must be met for the condition to be run. For example, you may want to process a step on a computer with Microsoft Office 2007 installed. Additionally, you may also want to further restrict the step to the Windows Vista operating system.  

> [!NOTE]
>  For the condition to be processed, the `SMS_TaskSequenceStep` class `Enabled` property must be set to `true`.  

 Within a task sequence step, the [SMS_TaskSequence_Step Server WMI Class](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) Condition property contains a [SMS_TaskSequence_Condition Server WMI Class](../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md) object that holds the condition. The condition is made up of one or more operands that are defined in an array of [SMS_TaskSequence_ConditionOperand Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md) derived classes by the `Operands` property. Each operand is an expression that must evaluate to `true`, for the step to be processed - a logical `and` operation.  

#### Expressions  
 Individual expressions are defined in [SMS_TaskSequence_ConditionExpression Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionexpression-server-wmi-class.md) derived classes.  

> [!NOTE]
>  `SMS_TaskSequence_ConditionExpression` derives from `SMS_TaskSequenceConditionOperand`.  

 For example, you would use [SMS_TaskSequence_SoftwareConditionExpression Server WMI Class](../../develop/reference/osd/sms_tasksequence_softwareconditionexpression-server-wmi-class.md) to define an expression for Microsoft Office 2007. The class used to define an expression for Windows Vista would be [SMS_TaskSequence_OSConditionGroup Server WMI Class](../../develop/reference/osd/sms_tasksequence_osconditiongroup-server-wmi-class.md).  

#### Nested Expressions  
 You can define more complex conditions containing nested expressions with [SMS_TaskSequence_ConditionOperator Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md). This class also derives from [SMS_TaskSequence_ConditionOperand Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md).  

 For example, you can form the condition `Exp1 and (Exp2 or Exp3)` by adding the following condition operands to a task sequence step's [SMS_TaskSequence_Condition Server WMI Class](../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md) instance's `Operand` array property.  

-   `SMS_TaskSequence_ConditionExpression` (`Exp1`).  

-   `SMS_TaskSequence_ConditionOperator` (nested expression `Exp2 or Exp3`).  

 The [SMS_TaskSequence_ConditionOperator Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md)`Operands` array property contains the expressions `Exp2` and `Exp3` and the [SMS_TaskSequence_ConditionOperator Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md)`Operator` property contains the desired operator. In this case `or`.  

> [!NOTE]
>  The operands in the task sequence step's [SMS_TaskSequence_Condition Server WMI Class](../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md)`Operand` array property are automatically compared with the `and` operator to evaluate the condition. The expressions in the `SMS_TaskSequence_ConditionOperator` must have an operator defined by the `Operator` property.  

 Since the [SMS_TaskSequence_Condition Server WMI Class](../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md)`Operands` property is an array of [SMS_TaskSequence_ConditionOperand Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md) classes, you can create more complex conditions such as `Exp1 and (Exp2 or (Exp3 and Exp4))`.  

 For more information about conditions, see [How to Add a Condition to an Operating System Deployment Task Sequence Step](../../develop/osd/how-to-add-a-condition-to-an-operating-system-deployment-task-sequence-step.md).  

## See Also  
 [SMS_TaskSequence_ConditionOperand Server WMI Class](../../develop/reference/osd/sms_tasksequence_conditionoperand-server-wmi-class.md)   
 [How to Add a Condition to an Operating System Deployment Task Sequence Step](../../develop/osd/how-to-add-a-condition-to-an-operating-system-deployment-task-sequence-step.md)
