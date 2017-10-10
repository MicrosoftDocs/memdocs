---
title: "Add a Step to an OS Deployment Group"
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
ms.assetid: 71c37f65-c745-4f17-88f0-5bed1ba14d82searchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Add a Step to an Operating System Deployment Group
You add a step (an action or a group) to an operating system deployment task sequence group, in System Center Configuration Manager, by adding the step to the `SMS_TaskSequenceGroup.Steps` array property.  

### To add a step to a task sequence group  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the [SMS_TaskSequenceGroup](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) object that you want to add the step to. For more information, see [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md).  

3.  Create the task sequence step. For an example of creating an action step, see [How to Add an Operating System Deployment Task Sequence Action](../../develop/osd/how-to-add-an-operating-system-deployment-task-sequence-action.md).  

4.  Add the step to the `SMS_TaskSequenceGroup.Steps` array property.  

5.  Reorder the step within the array property as necessary. For more information, see [How to Re-order an Operating System Deployment Task Sequence](../../develop/osd/how-to-reorder-an-operating-system-deployment-task-sequence.md)  

## Example  
 The following example method adds a command-line action to a task sequence group.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddStepToGroup(taskSequenceStep, group)     

    Dim steps   

    ' If needed, create a new steps array.  
    If IsNull(group.Steps) Then  
        steps = Array(taskSequenceStep)  
        group.Steps=steps  
    Else  
        ' Resize the existing steps and add step.  
        steps= Array(group.Steps)  
        ReDim steps (UBound (group.Steps)+1)   
        group.Steps(UBound(steps))=taskSequenceStep   
    End if   

End Sub  
```  

```c#  
public void AddStepToGroup(  
    WqlConnectionManager connection,   
    IResultObject taskSequence,   
    string groupName)  
{  
    try  
    {  
        // Get the group.  
        List<IResultObject> steps = taskSequence.GetArrayItems("Steps"); // Array of SMS_TaskSequence_Steps.  

        foreach (IResultObject ro in steps)  
        {  
            if (ro["Name"].StringValue == groupName && ro["__CLASS"].StringValue == "SMS_TaskSequence_Group")  
            {  
                IResultObject action = connection.CreateEmbeddedObjectInstance("SMS_TaskSequence_RunCommandLineAction");  
                action["CommandLine"].StringValue = @"C:\donowtingroup.bat";  
                action["Name"].StringValue = "Action in group " + groupName;  
                action["Description"].StringValue = "Action in a group";  
                action["Enabled"].BooleanValue = true;  
                action["ContinueOnError"].BooleanValue = false;  

                // Add the step to the task sequence.  
                List<IResultObject> array = ro.GetArrayItems("Steps");  

                array.Add(action);  

                ro.SetArrayItems("Steps", array);  
                taskSequence.SetArrayItems("Steps", steps);  
                break;  
            }  
        }  
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
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`taskSequence`<br /><br /> `taskSequenceStep`|-   Managed: `IResultObject`<br />-   VBScript: [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx)|-   A valid task sequence ([SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)) that contains the group.|  
|`groupName`<br /><br /> `group`|-   Managed: `String`<br />-   VBScript: `String`|The name of the group that the command-line action is added to. This is obtained from the `SMS_TaskSequenceGroup.Name` property.|  

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
 [How to Move a Step to a Different Operating System Deployment Task Sequence Group](../../develop/osd/how-to-move-a-step-to-a-different-task-sequence-group.md)   
 [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md)   
 [How to Remove a Step From an Operating System Deployment Group](../../develop/osd/how-to-remove-a-step-from-an-operating-system-deployment-group.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)
