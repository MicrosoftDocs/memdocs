---
title: "Custom Action Client Applications"
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
ms.assetid: b375eea9-ff01-4b23-913a-4d023715dbe6searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Configuration Manager Custom Action Client Applications
The task sequence application, in System Center Configuration Manager, performs the custom action operation during the client deployment. The application can be a process, a script, or other commands. The requirements for the application, such as the operating environment, command-line arguments, properties, and return codes are defined in a Managed Object Format (MOF) file. They are added to the task sequence environment when the action is processed.  

## Custom Action MOF File  
 The MOF file for a custom action is similar to the following:  

```  
[   CommandLine("smsswd.exe /run:%1 abc.exe %2"),  
    : (custom ui control and category qualifiers for action)  
    ]  
class MyCustomAction : SMS_TaskSequence_Action  
{  
    [TaskSequencePackage, CommandLineArg(1)]  
    string          PackageIDForAbcExe;  

    [CommandLineArg(2), AllowedLen("1-32000")]  
    string          AbcCommandLineArgs;  

    [SuccessCodes, Not_Null]  
    string          AbcSuccessCodes = "0 3010";  

    string         SomeOtherPropertyThatAbcNeeds;  

    string          SupportedEnvironment = "WinPEandFullOS";  
};  
```  

 The MOF file describes the information that is needed for the custom action application input, environment, properties and deployment package information.  

 For more information, see [About the Configuration Manager Custom Action MOF File](../../develop/osd/about-configuration-manager-custom-action-mof-files.md).  

## Application Input  
 Custom actions have to run unattended and therefore the application should not prompt for user input. All input should be received from either the command line, the task sequence environment, or from a data file.  

 The command-line for the action application is set, in the MOF file, by using the run command line built-in action.  

 For example:  

```  
CommandLine("smsswd.exe /run:PackageID abc.exe [any abc.exe command line args]"  
```  

## Application Processing  
 The task sequence application performs the custom action operations. It must be aware of its operating environment, be able to access the task sequencing environment variables, report progress, and return completion codes.  

### Environment  
 The MOF file should specify the operating environment with the [SMS_TaskSequence_Action Server WMI Class](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)`SupportedEnvironment` property. The available environments are Windows PE (`WinPE`), full operating system (`FullOS`), or both environments (`WinPEandFullOS`).  

 The choice of environment depends on the circumstances. For example, pre-operating install configuration will likely be done in the Windows PE environment. For more information, see [http://go.microsoft.com/fwlink/?LinkID=110498](http://go.microsoft.com/fwlink/?LinkID=110498). Updates to currently installed operating systems will use the full operating system environment. For example, software or driver installation. Operating system environment agnostic tasks such as reboots or the creation of network connections, can be performed by using both environment settings.  

### Processing  
 During processing, you access the task sequence variables defined by the MOF file by using the `TSEnvironment` COM automation object. For more information, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).  

 If the operation takes a long time, you can report progress to the task sequence environment and display a progress indicator by using the [ProgressUI Client COM Automation Class](../../develop/reference/core/clients/client-classes/progressui-client-com-automation-class.md). For more information, see [About Reporting Configuration Manager Custom Action Progress](../../develop/osd/about-reporting-configuration-manager-custom-action-progress.md).  

### Completion  
 The application should set the `SuccessCodes` environment variable as a return value when it is completed.  

|Return|Description|  
|------------|-----------------|  
|0|Success|  
|Non-zero|Failure|  

 If a reboot is required after the application finishes, the `SMSTSRebootRequested` environment variable should be set. For more information, see [http://go.microsoft.com/fwlink/?LinkId=110499](http://go.microsoft.com/fwlink/?LinkId=110498). For information about setting environment variables, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).  

## Deployment  
 To be used by System Center Configuration Manager, the custom action application must be available from a Configuration Manager package. The administrator can create the package by using either the Configuration Manager console or by using a programming language. For more information, see [How to Create a Package](../../develop/core/servers/configure/how-to-create-a-package.md).  

 The package identifier must be available for the deployment to work. Typically the MOF file declares a property to hold it, as in the following example:  

```  
[TaskSequencePackage, CommandLineArg(1)]  
string          PackageIDForAbcExe;  
```  

> [!NOTE]
>  The package identifier is the [SMS_Package Server WMI Class](../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)`PackageID` property.  

 The package identifier is obtained from the administrator, when the custom action is edited in the Task Sequence Editor.  

 To enable this, your custom action control can use a text edit control in its implementation to get the package identifier from the administrator. For an example that uses a text control, see [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md).  

 When used by the administrator, the custom action control is edited as part of a task sequence by using the Task Sequence Editor. When saved by the Task Sequence Editor, an [SMS_TaskSequencePackage Server WMI Class](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) is created to hold the task sequence, including the custom action.  

 The task sequence package is then advertised to clients along with the custom action package that is referenced by the custom action. For more information, see [How to Create an Advertisement](../../develop/core/servers/configure/how-to-create-an-advertisement.md).  

 When the custom action is run on the client, the package identifier for the custom action is supplied as a command-line parameter, from which the binary files for the custom action are extracted and run.  

-   The package identifier is provided by using the `/run` command-line parameter to Smsswd.exe.  

## Pre-Network Partition and Pre-Partition Setup  
 If you need to configure disk or network connectivity before you have a disk partition and before you have network connectivity, you will need to create an application to perform these tasks. Your application should be placed in a custom boot image by using the Windows Assessment and Deployment Kit. For more information, see TechNet documentation for the Windows Assessment and Deployment Kit ([http://go.microsoft.com/fwlink/?LinkId=111704](http://go.microsoft.com/fwlink/?LinkId=111704)).  

> [!NOTE]
>  Adding files to the boot image file can increase the minimum RAM requirements and can, due to low memory conditions, cause task sequences to fail in unexpected ways.  

 You will then need to import the image into System Center Configuration Manager as a custom image. For more information, see How to Add a Boot Image to Configuration Manager ([http://go.microsoft.com/fwlink/?LinkId=111706](http://go.microsoft.com/fwlink/?LinkId=111706)).  

 The application, any supporting files, and the custom SMSTS.INI should be placed in the Windows folder.  

 To use the application, you will use the custom boot image in a task sequence that contains a pre-partition/network step.  

## See Also  
 [About Configuration Manager Custom Actions](../../develop/osd/about-configuration-manager-custom-actions.md)   
 [About the Configuration Manager Custom Action MOF File](../../develop/osd/about-configuration-manager-custom-action-mof-files.md)   
 [Extending Operating System Deployment](../../develop/osd/extending-operating-system-deployment.md)
