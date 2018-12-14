---
title: "Create an OS Deployment Task Sequence"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 10cdc1b1-22b6-4d26-83e8-6f42580c985e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create an Operating System Deployment Task Sequence
You create a System Center Configuration Manager operating system deployment task sequence by creating an instance of the [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) class.  

 A task sequence contains one or more steps that are run sequentially on the client computer. For more information, see [Operating System Deployment Task Sequence Object Model](../../develop/osd/operating-system-deployment-task-sequence-object-model.md).  

 The task sequence is then packaged in an [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) and advertised to the client computer.  

### To create a task sequence  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create a task sequence `SMS_TaskSequence` object.  

3.  Add actions and, as required, add groups to the action. For more information, see [How to Add an Operating System Deployment Task Sequence Action](../../develop/osd/how-to-add-an-operating-system-deployment-task-sequence-action.md).  

4.  Associate the task sequence with a task sequence package. For more information, see [How to Create an Operating System Deployment Task Sequence Package](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-package.md).  

5.  Advertise the task sequence to the client computer. For more information, see [How to Create an Advertisement](../../develop/core/servers/configure/how-to-create-an-advertisement.md).  

## Example  
 The following example method creates a task sequence that installs a software program. The example also creates a task sequence package by calling the example that is defined in [How to Create an Operating System Deployment Task Sequence Package](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-package.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub CreateInstallSoftwareTaskSequence(connection,name, description, packageID, programName)  

    ' Create the task sequence.  
    set taskSequence = connection.Get("SMS_TaskSequence").SpawnInstance_  

    ' Create the action.  
    set action = connection.Get("SMS_TaskSequence_InstallSoftwareAction").SpawnInstance_  

    action.ProgramName=programName  
    action.PackageID=packageID  
    action.Name=name  
    action.Enabled=true  
    action.ContinueOnError=false  

    ' Create an array to hold the action.  
    actionSteps= array(action)  
    ' Add the array to the task sequence.  
    taskSequence.Steps=actionSteps  

    wscript.echo taskSequence.Steps(0).Name  
    call CreateTaskSequencePackage (connection, taskSequence)  

 End Sub  
```  

```c#  
public void CreateInstallSoftwareTaskSequence(  
    WqlConnectionManager connection,   
    string name,   
    string packageId,   
    string programName)  
{  
    try  
    {  
        // Create the task sequence.  
        IResultObject taskSequence = connection.CreateInstance("SMS_TaskSequence");  

        IResultObject ro = connection.CreateEmbeddedObjectInstance("SMS_TaskSequence_InstallSoftwareAction");  
        ro["ProgramName"].StringValue = programName;  
        ro["packageId"].StringValue = packageId;  
        ro["Name"].StringValue = name;  
        ro["Enabled"].BooleanValue = true;  
        ro["ContinueOnError"].BooleanValue = false;  

        // Add the step to the task sequence.  
        List<IResultObject> array = taskSequence.GetArrayItems("Steps");  

        array.Add(ro);  

        taskSequence.SetArrayItems("Steps", array);  

        // Create the task sequence package.  
        this.CreateTaskSequencePackage(connection, taskSequence);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to create Task Sequence: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`name`|-   Managed: `String`<br />-   VBScript:  `String`|The task sequence step name.|  
|`description`|-   VBScript:  `String`|The task sequence step description.|  
|`packageID`|-   Managed: `String`<br />-   VBScript:  `String`|The package identifier containing the software to be installed. Obtained from `SMS_Package.PackageID`.|  
|`programName`|-   Managed: `String`<br />-   VBScript:  `String`|The name of the program to be installed. Obtained from `SMS_Program.ProgramName`.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Objects](../../develop/core/understand/configuration-manager-objects.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)   
 [How to Create an Operating System Deployment Task Sequence Package](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-package.md)
