---
title: "Enumerate the Steps in an OS Deployment Task Sequence"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 6edec44e-6791-42f3-bf4d-5f3d3b78438a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Enumerate the Steps in an Operating System Deployment Task Sequence
You enumerate an operating system deployment task sequence, in System Center Configuration Manager, by using a recursive method to scan through the task sequence steps and groups.  

### To enumerate the steps in a task sequence  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Obtain a valid task sequence [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object. For more information, see [How to Create an Operating System Deployment Task Sequence](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence.md)  

3.  Enumerate through the steps to display any action ([SMS_TaskSequence_Action](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md)) names. Use recursion to access any groups ([SMS_TaskSequence_Group](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md)) that are found and display their actions.  

## Example  
 The following example displays the actions and groups within a task sequence.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub RecurseTaskSequenceSteps(taskSequence, indent)  

    Dim osdStep   
    Dim i  

    ' Indent each new group.  
    for each osdStep in taskSequence.Steps  

        for i=0 to indent  
            WScript.StdOut.Write " "  
        next  

        If osdStep.SystemProperties_("__CLASS")="SMS_TaskSequence_Group" Then  
            wscript.StdOut.Write "Group: "   
        End If  

        WScript.Echo osdStep.Name  

        ' Recurse into each group found.  
        If osdStep.SystemProperties_("__CLASS")="SMS_TaskSequence_Group" Then  
            If IsNull(osdStep.Steps) Then  
                Wscript.Echo "No steps"  
            Else  
                Call RecurseTaskSequenceSteps (osdStep, indent+3)  
            End If      
        End If  
     Next     
End Sub          
```  

```c#  
public void RecurseTaskSequenceSteps(  
    IResultObject taskSequence,  
    int indent)  
{  
    try  
    {  
        // The array of SMS_TaskSequence_Steps.  
        List<IResultObject> steps = taskSequence.GetArrayItems("Steps");  

        foreach (IResultObject ro in steps)  
        {  
            for (int i = 0; i < indent; i++)  
            {  
                Console.Write(" ");  
            }  

            if (ro["__CLASS"].StringValue == "SMS_TaskSequence_Group")  
            {  
                Console.Write("Group: ");  
            }  

            Console.WriteLine(ro["Name"].StringValue);  

            // Child groups that are found. Use recursion to view them.  
            if (ro["__CLASS"].StringValue == "SMS_TaskSequence_Group")  
            {  
                this.RecurseTaskSequenceSteps(ro, indent + 3);  
            }  
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
|`taskSequence`|-   Managed: `IResultObject`<br />-   VBScript: [SWbemObject](https://msdn.microsoft.com/library/aa393854.aspx)|A valid task sequence (`SMS_TaskSequence`). The group is added to this task sequence.|  
|`indent`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Indent is used to space console output for child groups.|  

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
