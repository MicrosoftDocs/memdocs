---
title: "Use Task Sequence Variables in a Running Task Sequence"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 2ed7e134-02da-4492-bb81-ce4a1f484955
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence
In Configuration Manager, you can create, get, and set task sequence variables in a running task sequence by using the task sequence environment COM automation object (`Microsoft.SMS.TSEnvironment`).  

 Typically, you use a command-line action that runs a script to access the task sequence variables. But you can also access them, within a running a task sequence, by using any programming environment that can use COM automation objects.  

> [!NOTE]
>  When you set a task variable on the Configuration Manager client, it becomes available to subsequent steps in the task sequence.  

 To create a custom task sequence variable, you set a `Microsoft.SMS.TSEnvironment` property by using the name of the new variable that you want to create. If the variable does not already exist, it is created. If the variable already exists, its value is updated. You can subsequently get the custom variable value from `Microsoft.SMS.TSEnvironment`.  

 When a task sequence variable is an array, it is passed in the following format:  

```  
<base array name><element #><Property>="value".  
```  

 For example, the `OSDPartitions` variable is an array of `SMS_TaskSequencePartitionSettings`. The following represents a one element `OSDPartitions` Array:  

```  
OSDPartitions0Bootable="true"  
OSDPartitions0FileSystem="NTFS"  
OSDPartition0QuickFormat="false"  
OSDPartitions0Size="100"  
OSDPartitions0SizeUnits="Percent"  
OSDPartitions0Type="Primary"  
```  

 To access `FileSystem` in this array, you would use `OSDPartitions0FileSystem`. If the array is larger, you would use`OSDPartitions1FileSystem` for the second element and so on through the array.  

 It is not recommended that you use managed code with the task sequencing environment because you cannot use it in the following environments:  

- Windows PE  

- Windows Server 2008  

- Windows 2000  

  Managed code does work when the full operating system is running with the correct version of .NET Framework installed.  

  The version of .NET Framework that is required depends on the version of Visual Studio that you use.  

|Visual Studio|.NET Framework Version|  
|-------------------|----------------------------|  
|Visual Studio 2003|1.0|  
|Visual Studio 2005|2.0|  
|Visual Studio 2008|2.0 to 3.5|  

 You will need to use COM interop to access the `TSEnvironment` object. You will need the following:  

-   Reference to **TSEnvironment 1.0 Type Library**.  

-   The **TSEnvironmentLib** namespace.  

### To use task variables in a running task sequence  

1.  In a running task sequence, create an instance of `Microsoft.SMS.TSEnvironment`.  

2.  Get or set the required environment variable.  

## Example  
 The following example method gets the `_SMSTSLogPath` variable. It also sets the value of a custom variable and an array custom variable value.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub UseTaskSequenceVariables()  
   dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
   dim logPath  

   ' You can query the environment to get an existing variable.  
   logPath = env("_SMSTSLogPath")  

    wscript.echo logPath   

   ' You can also set a variable in the Operating System Deployment environment.  
   env("MyCustomVariable") = "My Custom Value"  

   ' Set the OSDPartitions(0) Bootable array member to 0.  
    env("OSDPartitions0Bootable") = "true"  
End Sub  
```  

## Compiling the Code  

### Platforms  
 Operating System Deployment task sequencing environment  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [Objects overview](../core/understand/configuration-manager-objects-overview.md)
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Task sequence overview](operating-system-deployment-task-sequences-overview.md)
 [How to Set an Operating System Deployment Task Sequence Variable](../../develop/osd/how-to-set-an-operating-system-deployment-task-sequence-variable.md)
