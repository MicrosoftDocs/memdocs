---
title: "Remove a Step from an OS Deployment Group"
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
ms.assetid: 1c143409-2ecd-44ae-9517-f37c15e0acc3searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Remove a Step from an Operating System Deployment Group
In System Center Configuration Manager, you delete a step (an action or a group) from an operating system deployment task sequence group by deleting the step from the group's list of task sequence steps.  

### To remove a step from a group  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the [SMS_TaskSequence_Group](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) object that you want to add the step to. For more information, see [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md).  

3.  Remove the action from the SMS_TaskSequence_Group.Steps array property.  

## Example  
 The following example method removes an action from a task sequence group.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RemoveActionFromGroup(taskSequenceGroup, actionName)  

    Dim i  

    If taskSequenceGroup.SystemProperties_("__CLASS")<>"SMS_TaskSequence_Group" Then  
        wscript.echo "Not a group"  
        return  
    End If  

        Dim newArray  
        Dim actionStep  

        newArray = Array(taskSequenceGroup.Steps)  
        ReDim newArray(UBound(taskSequenceGroup.Steps))  

        i=0  
        for each  actionStep in taskSequenceGroup.Steps  
            If actionStep.Name = actionName and _  
              actionStep.SystemProperties_("__SUPERCLASS") = "SMS_TaskSequence_Action" Then  
                 ReDim preserve newArray(UBound(newArray)-1) ' shrink the Array  
            else  
               wscript.echo actionStep.Name  
               Set newArray(i)=actionStep ' copy it  
               i=i+1  
            End If     

         Next  

         taskSequenceGroup.Steps=newArray  

 End Sub  
```  

```c#  
public void RemoveActionFromGroup(  
    IResultObject taskSequenceGroup,   
    string actionName)  
{  
    try  
    {  
        if (taskSequenceGroup["__CLASS"].StringValue != "SMS_TaskSequence_Group")  
        {  
            throw new System.InvalidOperationException("Not a group");  
        }  

        List<IResultObject> groupSteps = taskSequenceGroup.GetArrayItems("Steps");  
        IResultObject actionFound = null;  
        foreach (IResultObject actionStep in groupSteps)  
        {  
            if (actionStep["Name"].StringValue == actionName && actionStep["__SUPERCLASS"].StringValue == "SMS_TaskSequence_Action")  
            {  
                actionFound = actionStep;  
                break;  
            }  
        }  

        groupSteps.Remove(actionFound);  
        taskSequenceGroup.SetArrayItems("Steps", groupSteps);  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to remove action: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`taskSequenceGroup`|-   Managed: IResultObject<br />-   VBScript: [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx)|The task sequence group containing the action to be deleted.|  
|`actionName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the action to be deleted. This can be obtained from the [SMS_TaskSequenceAction.Name](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md) property.|  

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
 [How to Add a Step  to an Operating System Deployment Group](../../develop/osd/how-to-add-a-step-to-an-operating-system-deployment-group.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Move a Step to a Different Operating System Deployment Task Sequence Group](../../develop/osd/how-to-move-a-step-to-a-different-task-sequence-group.md)   
 [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)
