---
title: "Set an OS Deployment Task Sequence Variable"
titleSuffix: "Configuration Manager"
description: In Configuration Manager, you create an operating system deployment task sequence variable by creating an instance of the SMS_TaskSequence_SetVariableAction class, adding to a task sequence.
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 47653e95-da5f-40c8-b4a7-11a90ad71452
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Set an Operating System Deployment Task Sequence Variable
In Configuration Manager, you create an operating system deployment task sequence variable by creating an instance of the [SMS_TaskSequence_SetVariableAction](../../develop/reference/osd/sms_tasksequence_setvariableaction-server-wmi-class.md) class, adding to a task sequence. You can also create task sequence variables while the task sequence is running on the client. For more information, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).  

 A task sequence variable is a name/value pair that you can access by task sequence steps. You can also create computer and collection-specific variables. For more information, see [How to Create a Collection Variable in Configuration Manager](../../develop/osd/how-to-create-a-collection-variable.md) and [How to Create a Computer Variable in Configuration Manager](../../develop/osd/how-to-create-a-computer-variable.md).  

> [!NOTE]
>  Variables that are set with the [SMS_TaskSequence_SetVariableAction](../../develop/reference/osd/sms_tasksequence_setvariableaction-server-wmi-class.md) class override variables that are set elsewhere. For example, if a collection variable and a SMS_TaskSequence_SetVariableAction have the same name, the value of the SMS_TaskSequence_SetVariableAction variable takes precedence.  

### To set a task sequence variable  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Get a task sequence to add the task sequence variable to. For more information, see [How to Create an Operating System Deployment Task Sequence](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence.md).  

3.  Create an instance of [SMS_TaskSequence_SetVariableAction](../../develop/reference/osd/sms_tasksequence_setvariableaction-server-wmi-class.md).  

4.  Set the VariableName and VariableValue properties for the variable that you are adding.  

5.  Add the SMS_TaskSequence_SetVariableAction object to the task sequence.  

## Example  
 The following example method sets a task sequence variable name and value.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddTaskSequenceVariable(connection, taskSequence, variableName, variableValue)     

    Dim variable  
    Dim steps  

    Set variable = connection.Get("SMS_TaskSequence_SetVariableAction").SpawnInstance_  

    variable.Name="MyTaskSequenceVariable"  
    variable.Description = "A task sequence variable"  
    variable.Enabled=True  
    variable.ContinueOnError=False  
    variable.VariableName=variableName  
    variable.VariableValue=variableValue  

    steps= Array(taskSequence.Steps)  

    ReDim steps (UBound (taskSequence.Steps)+1)    

    taskSequence.Steps(UBound(steps))=variable  

End Sub  
```  

```c#  
public void AddTaskSequenceVariable(  
    WqlConnectionManager connection,   
    IResultObject taskSequence,   
    string variableName,   
    string variableValue)  
{  
    try  
    {  
        // Create the task sequence variable object.  
        IResultObject variable = connection.CreateEmbeddedObjectInstance("SMS_TaskSequence_SetVariableAction");  

        // Populate the properties.  
        variable["Name"].StringValue = "MyTaskSequenceVariable";  
        variable["ContinueOnError"].BooleanValue = false;  
        variable["Description"].StringValue = "A task sequence variable set with SMS_TaskSequence_SetVariableAction";  
        variable["Enabled"].BooleanValue = true;  
        variable["VariableName"].StringValue = variableName;  
        variable["VariableValue"].StringValue = variableValue;  

        // Add the step to the task sequence.  
        List<IResultObject> array = taskSequence.GetArrayItems("Steps");  

        array.Add(variable);  
        taskSequence.SetArrayItems("Steps", array);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to set task sequence variable: " + e.Message);  
        throw;  
    }  
}  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|
|-|-|-|
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|-   A valid connection to the SMS Provider.|  
|`taskSequence`|-   Managed: `WqlConnectionManager`<br />-   VBScript: `SWbemServices`|-   The task sequence the variable is added to.|  
|`variableName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the variable.|  
|`variableValue`|-   Managed: `String`<br />-   VBScript: `String`|The value for the variable.|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [Objects overview](../core/understand/configuration-manager-objects-overview.md)
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Task sequence overview](operating-system-deployment-task-sequences-overview.md)
 [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)   
 [How to Read a Task Sequence from a Task Sequence Package](../../develop/osd/how-to-read-a-task-sequence-from-a-task-sequence-package.md)
