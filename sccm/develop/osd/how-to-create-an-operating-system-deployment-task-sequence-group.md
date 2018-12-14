---
title: "Create an OS Deployment Task Sequence Group"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4a4e9896-549e-4a20-92fc-30bf9ae6e1c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Create an Operating System Deployment Task Sequence Group
An operating system deployment task sequence group, in System Center Configuration Manager, can be added to a task sequence by creating an instance of the [SMS_TaskSequence_Group](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) class. The group is then added to the list of steps of the task sequence. The list of steps is an array of the [SMS_TaskSequence_Step](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md) derived classes. The array is stored in the task sequence, [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md), `Steps` property.  

### To create a task sequence group  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Obtain a valid task sequence ([SMS_TaskSequence)](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object. For more information, see [How to Create an Operating System Deployment Task Sequence](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence.md).  

3.  Create an instance of the `SMS_TaskSequence_Group` class.  

4.  Populate the group with the appropriate properties.  

5.  Update the task sequence `Steps` property with the new group.  

## Example  
 The following example method adds a new group to the supplied task sequence. Because the group is added to the end of the task sequence `Steps` array, you might want to reorder its position. For more information, see [How to Reorder an Operating System Deployment Task Sequence](../../develop/osd/how-to-reorder-an-operating-system-deployment-task-sequence.md).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddTaskSequenceGroup(connection, taskSequence, name, description)  

    Dim group    

    ' Create and populate the group.  
    Set group = connection.Get("SMS_TaskSequence_Group").SpawnInstance_  
    group.Name=name  
    group.Description=description  
    group.Enabled=True  
    group.ContinueOnError=False  

    ' Resize the task sequence steps array to hold the new group.  
    ReDim steps (UBound (taskSequence.Steps)+1)    

    ' Add the group.  
    taskSequence.Steps(UBound(steps))=group  

End Sub  
```  

```c#  
public IResultObject AddTaskSequenceGroup(  
    WqlConnectionManager connection,   
    IResultObject taskSequence,   
    string name,   
    string description)  
{  
    try  
    {  
        // Create the new group.  
        IResultObject ro = connection.CreateEmbeddedObjectInstance("SMS_TaskSequence_Group");  

        ro["Name"].StringValue = name;  
        ro["Description"].StringValue = description;  
        ro["Enabled"].BooleanValue = true;  
        ro["ContinueOnError"].BooleanValue = false;  

        // Add the group to the task sequence.  
        List<IResultObject> array = taskSequence.GetArrayItems("Steps");  
        array.Add(ro);  

        // Add the new group to the end of the current steps.  
        taskSequence.SetArrayItems("Steps", array);  

        return ro;  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to create Task Sequence: " + e.Message);  
        throw;  
    }  
}  
```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`taskSequence`|-   Managed: `IResultObject`<br />-   VBScript: [SWbemObject](https://msdn.microsoft.com/library/aa393741.aspx)|A valid task sequence (`SMS_TaskSequence`). The group is added to this task sequence.|  
|`Name`|-   Managed: `String`<br />-   VBScript: `String`|A name for the new group.|  
|`Description`|-   Managed: `String`<br />-   VBScript: `String`|A description for the new group.|  

|Parameter|Description|  
|---------------|-----------------|  
|`connection`|A `WqlConnectionManager` object that is a valid connection to the SMS Provider.|  
|`taskSequence`|An `IResultObject` that is a valid task sequence (`SMS_TaskSequence`). The group is added to this task sequence.|  
|`name`|A string name for the new group.|  
|`description`|A string description for the new group.|  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [Configuration Manager Operating System Deployment](../../develop/osd/operating-system-deployment.md)   
 [Configuration Manager Objects](../../develop/core/understand/configuration-manager-objects.md)   
 [Configuration Manager Programming Fundamentals](../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [How to Add a Step to an Operating System Deployment Group](../../develop/osd/how-to-add-a-step-to-an-operating-system-deployment-group.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create an Operating System Deployment Task Sequence](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)
