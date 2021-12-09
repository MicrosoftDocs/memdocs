---
title: Custom action client applications
titleSuffix: Configuration Manager
description: About custom action client applications.
ms.date: 10/01/2021
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# About Configuration Manager custom action client applications

The task sequence in Configuration Manager does custom action operations during client deployment. The application can be a process, a script, or other commands. The requirements for the application are defined in a Managed Object Format (MOF) file. Example requirements include the operating environment, command-line arguments, properties, and return codes. They're added to the task sequence environment when the action is processed.

## Custom action MOF file

The MOF file for a custom action is similar to the following example:

```mof
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

The MOF file describes the information that is needed for the custom action application input, environment, properties, and deployment package information.

For more information, see [About the Configuration Manager custom action MOF file](about-configuration-manager-custom-action-mof-files.md).

## Application input

Custom actions have to run unattended, so the application shouldn't prompt for user input. All inputs should be received from either the command line, the task sequence environment, or from a data file.

The command line for the action application is set, in the MOF file, by using the **Run command line** built-in action.

For example:

```mof
CommandLine("smsswd.exe /run:PackageID abc.exe [any abc.exe command line args]"
```

## Application processing

The task sequence application runs the custom action operations. It must be aware of its operating environment and have access to the task sequencing environment variables, report progress, and return completion codes.

### Environment

The MOF file should specify the operating environment with the [SMS_TaskSequence_Action Server WMI Class](../reference/osd/sms_tasksequence_action-server-wmi-class.md)`SupportedEnvironment` property. The available environments are Windows PE (`WinPE`), full operating system (`FullOS`), or both environments (`WinPEandFullOS`).

The choice of environment depends on the circumstances. For example, pre-operating install configuration will likely be done in the Windows PE environment. For more information, see [Infrastructure requirements for OS deployment](../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md). Updates to currently installed operating systems will use the full operating system environment. For example, software or driver installation. Operating system environment agnostic tasks such as reboots or the creation of network connections, can be performed by using both environment settings.

### Processing

During processing, you access the task sequence variables defined by the MOF file by using the `TSEnvironment` COM automation object. For more information, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](how-to-use-task-sequence-variables-in-a-running-task-sequence.md).

If the operation takes a long time, you can report progress to the task sequence environment and display a progress indicator by using the [ProgressUI client COM automation class](../reference/core/clients/client-classes/progressui-client-com-automation-class.md). For more information, see [About reporting Configuration Manager custom action progress](about-reporting-configuration-manager-custom-action-progress.md).

### Completion

The application should set the `SuccessCodes` environment variable as a return value when it's completed.

| Return | Description |
|--|--|
| 0 | Success |
| Non-zero | Failure |

If a reboot is required after the application finishes, the `SMSTSRebootRequested` environment variable should be set. For more information, see [Task sequence variables](../../osd/understand/task-sequence-variables.md#SMSTSRebootRequested). For information about setting environment variables, see [How to use task sequence variables in a running Configuration Manager task sequence](how-to-use-task-sequence-variables-in-a-running-task-sequence.md).

## Deployment

To be used by Configuration Manager, the custom action application must be available from a Configuration Manager package. The administrator can create the package by using either the Configuration Manager console or by using a programming language. For more information, see [How to create a package](../core/servers/configure/how-to-create-a-package.md).

The package identifier must be available for the deployment to work. Typically the MOF file declares a property to hold it, as in the following example:

```mof
[TaskSequencePackage, CommandLineArg(1)]
string PackageIDForAbcExe;
```

> [!NOTE]
> The package identifier is the [SMS_Package Server WMI Class](../reference/core/servers/configure/sms_package-server-wmi-class.md)`PackageID` property.

The package identifier is obtained from the administrator, when the custom action is edited in the task sequence editor.

To enable this behavior, your custom action control can use a text edit control in its implementation to get the package identifier from the administrator. For an example that uses a text control, see [How to create a Configuration Manager custom action control](how-to-create-a-configuration-manager-custom-action-control.md).

When used by the administrator, the custom action control is edited as part of a task sequence by using the task sequence editor. When saved by the task sequence editor, an [SMS_TaskSequencePackage Server WMI Class](../reference/osd/sms_tasksequencepackage-server-wmi-class.md) is created to hold the task sequence, including the custom action.

The task sequence package is then advertised to clients along with the custom action package that is referenced by the custom action. For more information, see [How to create an advertisement](../core/servers/configure/how-to-create-an-advertisement.md).

When the custom action is run on the client, the package identifier for the custom action is supplied as a command-line parameter, from which the binary files for the custom action are extracted and run.

The package identifier is provided by using the `/run` command-line parameter to Smsswd.exe.

## Pre-network partition and pre-partition setup

If you need to configure disk or network connectivity before you have a disk partition and before you have network connectivity, you need to create an application to do these tasks. Your application should be placed in a custom boot image by using the Windows Assessment and Deployment Kit (ADK). For more information, see [Windows ADK scenarios for IT Pros](/windows/deployment/windows-adk-scenarios-for-it-pros).

> [!NOTE]
> Adding files to the boot image file can increase the minimum RAM requirements and can, due to low memory conditions, cause task sequences to fail in unexpected ways.

Then import the image into Configuration Manager as a custom image. For more information, see [Add a boot image](../../osd/get-started/manage-boot-images.md#add-a-boot-image).

The application, any supporting files, and the custom SMSTS.INI should be placed in the Windows folder.

To use the application, use the custom boot image in a task sequence that contains a pre-partition/network step.

## See also

[About Configuration Manager custom actions](about-configuration-manager-custom-actions.md)

[About the Configuration Manager custom action MOF file](about-configuration-manager-custom-action-mof-files.md)
