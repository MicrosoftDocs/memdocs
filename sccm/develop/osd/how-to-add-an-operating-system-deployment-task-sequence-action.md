---
title: "Add an OS Deployment Task Sequence Action | Microsoft Docs"
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
ms.assetid: b03f13c1-d358-455b-a684-0bd8e8bd940a
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Add an Operating System Deployment Task Sequence Action
An operating system deployment task sequence action is added to a task sequence, in System Center Configuration Manager, by creating an instance of an [SMS_TaskSequence_Action](assetId:///SMS_TaskSequence_Action?qualifyHint=False&autoUpgrade=True) derived class and then adding it to the steps of the task sequence.  

> [!NOTE]
>  System Center Configuration Manager has a number of built-in actions that you can use. For example the command-line action class is [SMS_TaskSequence_RunCommandLineAction](assetId:///SMS_TaskSequence_RunCommandLineAction?qualifyHint=False&autoUpgrade=True). These classes derive from the assetId:///SMS_TaskSequence_Action?qualifyHint=False&autoUpgrade=True class.  

 [SMS_TaskSequenceAction](assetId:///SMS_TaskSequenceAction?qualifyHint=False&autoUpgrade=True) derives from the  [SMS_TaskSequence_Step](assetId:///SMS_TaskSequence_Step?qualifyHint=False&autoUpgrade=True) class, which is the base class for both actions and groups. The task sequence stores its steps in an array of assetId:///SMS_TaskSequence_Step?qualifyHint=False&autoUpgrade=True, thus allowing actions and groups to be stored together.  

### To add a task sequence action  

1.  Set up a connection to the SMS Provider. For more information see, [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create a task sequence ([SMS_TaskSequence](assetId:///SMS_TaskSequence?qualifyHint=False&autoUpgrade=True)) object. For more information, see [How to Create an Operating System Deployment Task Sequence](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence.md).  

3.  Create an assetId:///SMS_TaskSequenceAction?qualifyHint=False&autoUpgrade=True derived class instance, for example, [SMS_TaskSequence_RunCommandLine](assetId:///SMS_TaskSequence_RunCommandLine?qualifyHint=False&autoUpgrade=True), for the action you want.  

4.  Populate the action as appropriate.  

5.  Add the action to the task sequences steps. This is stored the assetId:///SMS_TaskSequence?qualifyHint=False&autoUpgrade=True class [Steps](assetId:///Steps?qualifyHint=False&autoUpgrade=True) property.  

## Example  
 The following example method creates a command-line action and adds it to the supplied task sequence.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddTaskSequenceActionCommandLine(connection, taskSequence, name, description)     

    Dim steps  
    Dim action    

    Set action = connection.Get("SMS_TaskSequence_RunCommandLineAction").SpawnInstance_  

    action.CommandLine = "cmd /c Echo Hello"  
    action.Name=name  
    action.Description=description  
    action.Enabled=True  
    action.ContinueOnError=False  

      If IsNull(taskSequence.Steps) Then  
        steps = Array(action)  
        taskSequence.Steps=steps  
    Else  
        steps= Array(taskSequence.Steps)  
        ReDim steps (UBound (taskSequence.Steps)+1)   
        taskSequence.Steps(UBound(steps))=action  
    End if    

End Sub  

```  

```c#  
public IResultObject AddTaskSequenceActionCommandLine(  
    WqlConnectionManager connection,   
    IResultObject taskSequence,  
    string name,   
    string description)  
{  
    try  
    {  
        // Create the new step.  
        IResultObject ro;  

        ro = connection.CreateEmbeddedObjectInstance("SMS_TaskSequence_RunCommandLineAction");  
        ro["CommandLine"].StringValue = @"cmd /c Echo Hello";  

        ro["Name"].StringValue = name;  
        ro["Description"].StringValue = description;  
        ro["Enabled"].BooleanValue = true;  
        ro["ContinueOnError"].BooleanValue = false;  

        // Add the step to the task sequence.  
        List<IResultObject> array = taskSequence.GetArrayItems("Steps");  

        array.Add(ro);  

        taskSequence.SetArrayItems("Steps", array);  

        return ro;  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to add action: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: [WqlConnectionManager](assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True)<br />-   VBScript: [SWbemServices](assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True)|A valid connection to the SMS Provider.|  
|`taskSequence`|-   Managed: [IResultObject](assetId:///IResultObject?qualifyHint=False&autoUpgrade=True)<br />-   VBScript: [SWbemObject](assetId:///SWbemObject?qualifyHint=False&autoUpgrade=True)|A valid task sequence (assetId:///SMS_TaskSequence?qualifyHint=False&autoUpgrade=True).|  
|`Name`|-   Managed: `String`<br />-   VBScript: `String`|A name for the new action.|  
|`Description`|-   Managed: `String`<br />-   VBScript: `String`|A description for the action.|  

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
 [How to Add a Condition to an Operating System Deployment Task Sequence Step](../../develop/osd/how-to-add-a-condition-to-an-operating-system-deployment-task-sequence-step.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [How to Create an Operating System Deployment Task Sequence Group](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-group.md)   
 [How to Delete an Operating System Deployment Task Sequence Action](../../develop/osd/how-to-delete-an-operating-system-deployment-task-sequence-action.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)
