---
title: "Reorder an OS Deployment Task Sequence"
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
ms.assetid: 1f01d10f-1aff-4f56-9f23-b53f222a57e9searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Reorder an Operating System Deployment Task Sequence
In System Center Configuration Manager, you can reorder the steps (an action or a group) in a task sequence or group by rearranging the step sequence in the [Steps](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) property [SMS_TaskSequence_Step](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) array.  

### To reorder a task sequence  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Obtain a valid task sequence ([SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)) or task sequence group ([SMS_TaskSequence_Group](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md)). For more information, see [How to Read a Task Sequence From a Task Sequence Package](../../develop/osd/how-to-read-a-task-sequence-from-a-task-sequence-package.md).  

3.  Within the `Steps` array property, move the [SMS_TaskSequence_Step](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) to its new location.  

4.  Update the task sequence or group.  

## Example  
 The following example shows how to move a step up or down within a task sequence or group.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub MoveTaskSequenceStepDown(taskSequence, stepName)  
   Dim index  
   Dim osdStep  
   Dim temp  

    index=0  

    ' If found, move the step down.  
    for each osdStep in taskSequence.Steps  
        If osdStep.Name=stepName Then  
            If index < Ubound (TaskSequence.Steps) Then  
                Set temp=osdStep  
                taskSequence.Steps(index)=taskSequence.Steps(index+1)  
                taskSequence.Steps(index+1)=temp  
                Exit For  
           End If      
        End If  

        index=index+1  
    next  
End Sub  

Sub MoveTaskSequenceStepUp(taskSequence, stepName)  
    Dim index  
    Dim osdStep  
    Dim temp       

    index=0  

    ' If found, move the step up.  
    for Each osdStep In taskSequence.Steps  
        If osdStep.Name=stepName Then  
            If index >1 Then  
                Set temp=osdStep  
                taskSequence.Steps(index)=taskSequence.Steps(index-1)  
                taskSequence.Steps(index-1)=temp  
                Exit For  
           End If      
        End If  

        index=index+1  

    next  
End Sub  
```  

```c#  
public void MoveTaskSequenceStepDown(  
    IResultObject taskSequence,   
    string taskSequenceStepName)  
{  
    try  
    {  
        // Get the task sequence steps.  
        List<IResultObject> steps = taskSequence.GetArrayItems("Steps"); // Array of SMS_TaskSequence_Steps.  

        int index = 0;  

        // Scan through the steps to find the step to move down.  
        foreach (IResultObject ro in steps)  
        {  
            if (ro["Name"].StringValue == taskSequenceStepName)  
            {  
                // Move the step.  
                if (index < steps.Count - 1) // Not at end, so we can flip.  
                {  
                    steps.Insert(index + 2, steps[index]);  
                    steps.Remove(steps[index]);  
                    taskSequence.SetArrayItems("Steps", steps);  
                    break;  
                }  
            }  

            index++;  
        }  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed To enumerate task sequence items: " + e.Message);  
        throw;  
    }  
}  

public void MoveTaskSequenceStepUp(  
    IResultObject taskSequence,   
    string taskSequenceStepName)  
{  
    try  
    {  
        // Get the task sequence steps.  
        List<IResultObject> steps = taskSequence.GetArrayItems("Steps"); // Array of SMS_TaskSequence_Steps.  

        int index = 0;  

        foreach (IResultObject ro in steps)  
        {  
            if (ro["Name"].StringValue == taskSequenceStepName)  
            {  
                if (index > 0) // Not the first step, so you can move it up.  
                {  
                    steps.Insert(index + 1, steps[index - 1]);  
                    steps.Remove(steps[index - 1]);  
                    taskSequence.SetArrayItems("Steps", steps);  
                    break;  
                }  
            }  
            index++;  
        }  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed To enumerate task sequence items: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`taskSequence`|-   Managed: `IResultObject`<br />-   VBScript: [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx)|A valid task sequence or task sequence group|  
|`taskSequenceStepName`<br /><br /> `stepName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the task sequence step to move.|  

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
 [How to Add an Operating System Deployment Task Sequence Action](../../develop/osd/how-to-add-an-operating-system-deployment-task-sequence-action.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)
