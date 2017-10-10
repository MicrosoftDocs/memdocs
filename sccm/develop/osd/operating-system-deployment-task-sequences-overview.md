---
title: "OS Deployment Task Sequences Overview"
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
ms.assetid: 957ac65f-a14b-4659-84b8-b83190698cc7searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Operating System Deployment Task Sequences Overview
In System Center Configuration Manager, a task sequence is a series of one or more task steps that can be advertised to Configuration Manager clients to run user-specified actions. Task sequences are used with operating system deployment to build source computers, capture an operating system image, migrate user and computer settings, and deploy an image to a collection of target computers. Task sequences can also be used to run other Configuration Manager actions, such as deploying Configuration Manager software packages or running custom command lines.  

 Configuration Manager provides a rich Windows Management Instrumentation (WMI) object model for creating and editing task sequences. For more information, see [Operating System Deployment Task Sequence Object Model](../../develop/osd/operating-system-deployment-task-sequence-object-model.md).  

## Task Sequence Steps  
 A task sequence step is either an individual action that is run on a computer, such as a running a command line, or it is a set of actions arranged in a group. Task steps are processed in order and can have conditions associated with them that determine whether the action, or group of actions, is processed.  

## Actions  
 There are two types of actions: built in action and custom actions.  

### Built-in Actions  
 A Configuration Manager action that performs a specific action on the Configuration Manager client computer is a built-in action. For example, Configuration Manager provides built-in actions for partitioning disks and also for installing software. For more information about the Configuration Manager built in actions, see the Configuration Manager documentation library.  

 There is also a command-line action that the administrator can use for running scripts or executable files on the Configuration Manager client computer.  

### Custom Actions  
 An action that you create yourself is a custom action. You can create custom actions that call a process or script that you define in a Managed Object Format (MOF) file. You can also create a control that integrates the custom action you create into the task sequence editor. This allows the administrator to change custom action properties in the same way that the System Center Configuration Manager supplied actions are changed. Typically, you create these custom actions when the built-in actions do not satisfy your requirements for an action. For more information about creating custom actions, see [About Configuration Manager Custom Actions](../../develop/osd/about-configuration-manager-custom-actions.md).  

## Running Task Sequences  
 To run a task sequence, you must perform the following:  

#### To run a task sequence  

1.  Ensure that you have the Configuration Manager site server installed and that you have clients to deploy task sequences to. Depending on your environment, you might need to configure the State Migration Point or PXE Service Point. For more information, see [Operating System Deployment Site Role Configuration](../../develop/osd/operating-system-deployment-site-role-configuration.md).  

2.  Create a package containing the files you need for deployment. For example, to deploy a boot image you will need to create a boot image package ([SMS_BootImagePackage Server WMI Class](../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)).  

3.  Assign the package to a distribution point. For more information, see [How to Assign a Package to a Distribution Point](../../develop/core/servers/configure/how-to-assign-a-package-to-a-distribution-point.md).  

4.  Create a task sequence. For more information, see  [How to Create an Operating System Deployment Task Sequence](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence.md).  

5.  Associate the task sequence with a task sequence package. For more information, see [How to Create an Operating System Deployment Task Sequence Package](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-package.md).  

6.  Advertise the task sequence package to the required client computers. To do this you create an [SMS_Advertisement](../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) package. If you want to show a task sequence progress dialog box while the task sequence runs, set the [SMS_Advertisement](../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md) class `AdvertFlags` show task sequence progress bit (0x00800000). For more information, see [About Software Distribution Advertisements](../../develop/core/servers/configure/about-software-distribution-deployments.md).  

7.  On the client computer, the task sequence is eventually available as an advertised program. Click the program to run it.  

## Detecting a Failed Task Sequence  
 When a task sequence runs, you can use the `_SMSTSLastActionSucceeded` variable to determine if the last task sequence group run has failed. Depending on the environment the task sequence is running in, you can then take appropriate action. Typically you will copy the task logs to a share for inspection.  

#### To detect a failed task sequence  

1.  Set the continue on error property for the task sequence group that you want to detect failure on.  

2.  Immediately after the group, create a group to handle the error.  

3.  In the error handler group, Add a condition that runs the error handler group if `_SMSTLastActionSucceeded` = `false`.  

4.  In the error handler group, add a Run Command Line action. This will be used for error handling in a WinPE environment.  

5.  In the WinPE action, add the following command line to copy the log to an external share: `smsswd.exe /run: cmd /c copy x:\windows\temp\smsts.log \\<Your server>\<Your Share>\%_SMSTSClientGuid%-smsts.log`  

6.  In the WinPE action, add a condition that runs the action if `_SMSTSInWinPE` is true.  

7.  In the error handler group, add a run command-line action. This will be used for error handling in a full operating system environment.  

8.  In the full operating system action, add the following command line to copy the log to an external share: `smsswd.exe /run: cmd /c copy %windir%\system32\ccm\logs\smsts.log \\server\share\%_SMSTSClientGuid%-smsts.log`  

9. In the WinPE action, add a condition that runs the action if `_SMSTSInWinPE` is false.  

10. In the error handler group, add a run command-line action and a command line that runs a recovery tool of your choosing.  

## Pre-Execution Hooks  
 You can run scripts or executables that can interact with the user in Windows PE before the task sequence is selected. For more information, see Operating System Media Pre-Execution Hook in the Configuration Manager library documentation.  

## Securing Task Sequences  
 A task sequence package ([SMS_TaskSequencePackage Server WMI Class](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)) is secured by using the [SMS_UserClassPermissions Server WMI Class](../../develop/reference/misc/sms_userclasspermissions-server-wmi-class.md) and [SMS_UserInstancePermissionInfo Server WMI Class](../../develop/reference/misc/sms_userinstancepermissioninfo-server-wmi-class.md) permissions to set class and instance permissions.  

## See Also  
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Operating System Deployment Task Sequence Object Model](../../develop/osd/operating-system-deployment-task-sequence-object-model.md)
