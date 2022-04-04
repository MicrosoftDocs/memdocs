---
title: "Add a Condition to an OS Deployment Task Sequence Step"
titleSuffix: "Configuration Manager"
description: "How to Add a Condition to an Operating System Deployment Task Sequence Step"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 153b47c9-14fc-4b09-a2d7-99e0de5b6759
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Add a Condition to an Operating System Deployment Task Sequence Step
Conditions can be added to an operating system deployment step (action and group), in Configuration Manager, by creating a [SMS_TaskSequence_Condition](../../develop/reference/osd/sms_tasksequence_condition-server-wmi-class.md) class instance and then associating it with the step. If the condition operands are all met, then the step is processed; otherwise it is not. The condition can have one or more operands that are instances of SMS_TaskSequence_Condition derived classes. You specify operators for the operands with instances of [SMS_TaskSequence_ConditionOperator](../../develop/reference/osd/sms_tasksequence_conditionoperator-server-wmi-class.md).  

### To add a condition to a step  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md).  

2.  Obtain a task sequence step object. This can be an [SMS_TaskSequence_Group](../../develop/reference/osd/sms_tasksequence_group-server-wmi-class.md) object for a group, or a  [SMS_TaskSequenceAction](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md) derived class object for an action, for more information, see [How to Add an Operating System Deployment Task Sequence Action](../../develop/osd/how-to-add-an-operating-system-deployment-task-sequence-action.md).  

3.  Create a new condition by creating an instance of `SMS_TaskSequence_Condition`.  

4.  Create an expression for the condition by creating an instance of an [SMS_TaskSequence_ConditionExpression](../../develop/reference/osd/sms_tasksequence_conditionexpression-server-wmi-class.md) derived class. For example, [SMS_TaskSequence_RegistryConditionExpression](../../develop/reference/osd/sms_tasksequence_registryconditionexpression-server-wmi-class.md).  

5.  Populate the expression properties.  

6.  Add the expression to the condition *Operands* property.  

7.  Add the condition to the task sequence step class *Condition* property.  

## Example  
 The following example method adds a condition to a supplied step that determines if the HKEY_LOCAL_MACHINE\MICROSOFT registry key exists. The SMS_TaskSequenc_RegistryCondition Expression is used to specify the condition.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub AddRegistryCondition (connection, taskSequenceStep)  

    Dim condition  
    Dim registryExpression  
    Dim operands  

    ' Get or create the condition.  
    if IsNull ( taskSequenceStep.Condition) Then  
       Set condition = connection.Get("SMS_TaskSequence_Condition").SpawnInstance_  
    Else  
        Set condition = taskSequenceStep.Condition  
    End If     

    ' Populate the condition.  
    Set registryExpression=connection.Get("SMS_TaskSequence_RegistryConditionExpression").SpawnInstance_  
    registryExpression.KeyPath="HKEY_LOCAL_MACHINE\MICROSOFT"  
    registryExpression.Operator="exists"  
    registryExpression.Type="REG_SZ"  
    registryExpression.Data=Null  

    ' Add the condition.  
    operands=Array(registryExpression)  
    condition.Operands=operands  
    taskSequenceStep.Condition=condition  

End Sub  
```  

```c#  
public void AddRegistryCondition(  
    WqlConnectionManager connection,   
    IResultObject taskSequenceStep)  
{  
    try  
    {  
        IResultObject condition;  

        if (taskSequenceStep["Condition"].ObjectValue == null)  
        {  
            // Create a new condition.  
            condition = connection.CreateEmbeddedObjectInstance("SMS_TaskSequence_Condition");  
        }  
        else  
        {   // Get the existing condition.  
            condition = taskSequenceStep.GetSingleItem("Condition");  
        }  

        // Create and populate the expression.  
        IResultObject registryExpression = connection.CreateEmbeddedObjectInstance("SMS_TaskSequence_RegistryConditionExpression");  

        registryExpression["KeyPath"].StringValue = @"HKEY_LOCAL_MACHINE\MICROSOFT";  
        registryExpression["Operator"].StringValue = "exists";  
        registryExpression["Type"].StringValue = "REG_SZ";  
        registryExpression["Data"].StringValue = null;  

        // Get the operands and add the expression.  
        List<IResultObject> operands = condition.GetArrayItems("Operands");  
        operands.Add(registryExpression);  

        // Add the expresssion to the list of operands.  
        condition.SetArrayItems("Operands", operands);  

        // Add the condition to the sequence.  
        taskSequenceStep.SetSingleItem("Condition", condition);  
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
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`taskSequenceStep`|-   Managed: `IResultObject`<br />-   VBScript:  [SWbemObject](/windows/win32/wmisdk/swbemobject)|A valid task sequence step ([SMS_TaskSequenceStep](../../develop/reference/osd/sms_tasksequence_step-server-wmi-class.md)).|  

## Compiling the Code  
 The C# example has the following compilation requirements:  

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
 [How to Add an Operating System Deployment Task Sequence Action](../../develop/osd/how-to-add-an-operating-system-deployment-task-sequence-action.md)   
 [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to an SMS Provider in Configuration Manager  by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [Task sequence overview](operating-system-deployment-task-sequences-overview.md)
