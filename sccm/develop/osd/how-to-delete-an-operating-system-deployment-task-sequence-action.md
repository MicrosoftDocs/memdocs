---
title: "Delete an OS Deployment Task Sequence Action"
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
ms.assetid: 32db0107-f390-4324-9c36-e60976edf9ebsearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete an Operating System Deployment Task Sequence Action
You delete an operating system deployment task sequence action, in System Center Configuration Manager, by removing the action from the task sequence steps.  

### To delete a task sequence action  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Obtain a task sequence ([SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)) object. For more information, see [How to Create an Operating System Deployment Task Sequence](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence.md).  

3.  Remove the action from the `SMS_TaskSequence.Steps` array property.  

## Example  
 The following example method deletes an action from the task sequence. The action is identified as an action by checking the Windows Management Instrumentation (WMI) property \__SUPERCLASS to ensure it derives from [SMS_TaskSequenceAction](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RemoveAction (connection, taskSequence, actionName)  

    Dim i  
    Dim newArray  
    Dim actionStep  

    If taskSequence.SystemProperties_("__CLASS")<>"SMS_TaskSequence" Then  
        wscript.echo "Not a task sequence"  
        Exit Sub  
    End If  

    if IsNull(taskSequence.Steps) Then  
        Wscript.Echo "No steps"  
        Exit Sub  
    End If  

    ' Create an array to hold copied steps.  
    newArray = Array(taskSequence.Steps)  
    ReDim newArray(UBound(taskSequence.Steps))  

    ' Copy the steps into the array and remove the matching action.  
    i=0  
    for each  actionStep in taskSequence.Steps  
        If actionStep.Name = actionName and _  
          actionStep.SystemProperties_("__SUPERCLASS") = "SMS_TaskSequence_Action" Then  
             ReDim preserve newArray(UBound(newArray)-1) ' shrink the Array  
        else  
           Set newArray(i)=actionStep ' copy it  
           i=i+1  
        End If     
     Next  

     ' Assign new array back to the task sequence.  
     taskSequence.Steps=newArray           

End Sub      
```  

```c#  
public void RemoveAction(  
    IResultObject taskSequence,   
    string actionName)  
{  
    try  
    {  
        // Get a list of steps.  
        List<IResultObject> actionSteps = taskSequence.GetArrayItems("Steps");  

        // Find the action to be deleted.  
        foreach (IResultObject actionStep in actionSteps)  
        {  
            if (actionStep["Name"].StringValue == actionName && actionStep["__SUPERCLASS"].StringValue == "SMS_TaskSequence_Action")  
            {  
                // Delete the action.  
                actionSteps.Remove(actionStep);  
                break;  
            }  
        }  

        // Update the task sequence.  
        taskSequence.SetArrayItems("Steps", actionSteps);  
    }  
    catch (Exception e)  
    {  
        Console.WriteLine("Failed to remove action: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed:`WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`taskSequence`|-   Managed: `IResultObject`<br />-   VBScript:  [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx)|The task sequence containing the action to be deleted.|  
|`actionName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the action to be deleted. This can be obtained from the `SMS_TaskSequenceAction.Name` property.|  

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
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)
