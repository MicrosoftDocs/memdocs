---
title: "Move a Step to a Different OS Deployment Task Sequence Group"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: f93360ef-677e-48e0-886a-a07b8451611c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Move a Step to a Different Operating System Deployment Task Sequence Group
You move a step (an action or a group) from one operating system deployment task sequence group to another, in Configuration Manager, by adding the step to the target group and then by deleting the step from the source group.  

### To move a step from one group to another  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Get the source and target [SMS_TaskSequenceGroup](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) objects. Copy a step that you want to add the step to. For more information, see [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md).  

3.  Add the step to the target group. For more information, see [How to Add a Step to an Operating System Deployment Group](../../develop/osd/how-to-add-a-step-to-an-operating-system-deployment-group.md).  

4.  Reorder the step within the target group array property as necessary. For more information, see [How to Re-order an Operating System Deployment Task Sequence](../../develop/osd/how-to-reorder-an-operating-system-deployment-task-sequence.md)  

5.  Delete the step from the source group. For more information, see [How to Remove a Step From an Operating System Deployment Group](../../develop/osd/how-to-remove-a-step-from-an-operating-system-deployment-group.md).  

## Example  
 The following example method moves a step from one task sequence group to another.  

 You will need the code snippet in [How to Remove a Step From an Operating System Deployment Group](../../develop/osd/how-to-remove-a-step-from-an-operating-system-deployment-group.md) to run this example.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub MoveActionToGroup( taskSequenceStep, sourceGroup,targetGroup)  

        Dim steps  
        Dim groupSteps   

        Steps = Array(targetGroup.Steps)  

        If IsNull(targetGroup.Steps) Then  
            groupSteps = Array(taskSequenceStep)  
            targetGroup.Steps = groupSteps  
        Else      
            ReDim steps (UBound (targetGroup.Steps)+1)    
            targetGroup.Steps(UBound(steps))=taskSequenceStep  
        End If      

        Call RemoveActionFromGroup(sourceGroup,taskSequenceStep.Name)  

End Sub  
```  

```c#  
public void MoveActionToGroup(  
    IResultObject taskSequenceStep,   
    IResultObject sourceGroup,   
    IResultObject targetGroup)  
{  
    try  
    {  
        // Add the step to the target group.   
        // Note. You can use MoveTaskSequenceStepUp and MoveTaskSequenceStepDown  
        // to place the step in the target group.  

        List<IResultObject> groupSteps = targetGroup.GetArrayItems("Steps");  
        groupSteps.Add(taskSequenceStep);  
        targetGroup.SetArrayItems("Steps", groupSteps);  

        // Remove action from the source group.  
        this.RemoveActionFromGroup(sourceGroup, taskSequenceStep["Name"].StringValue);  
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
|`taskSequenceStep`|-   Managed: `IResultObject`<br />-   VBScript: [SWbemObject](/windows/win32/wmisdk/swbemobject)|A valid task sequence step (Group or action) ([SMS_TaskSequence_Step](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md)).|  
|`sourceGroup`|-   Managed: `IResultObject`<br />-   VBScript: `SWbemObject`|The group `SMS_TaskSequenceGroup` the step is copied from.|  
|`targetGroup`|-   Managed: `IResultObject`<br />-   VBScript: `SWbemObject`|The group `SMS_TaskSequenceGroup` the step is copied to.|  

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
 [How to Add a Step  to an Operating System Deployment Group](../../develop/osd/how-to-add-a-step-to-an-operating-system-deployment-group.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md)   
 [How to Remove a Step From an Operating System Deployment Group](../../develop/osd/how-to-remove-a-step-from-an-operating-system-deployment-group.md)   
 [Task sequence overview](operating-system-deployment-task-sequences-overview.md)
