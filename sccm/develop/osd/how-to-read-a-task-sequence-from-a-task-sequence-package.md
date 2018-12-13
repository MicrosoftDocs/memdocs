---
title: "Read a Task Sequence from a Task Sequence Package"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 222d153e-50d4-4572-b2b1-6a0d131c998b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Read a Task Sequence from a Task Sequence Package
You read a task sequence from a task sequence package, in System Center Configuration Manager, by calling the [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) class [GetSequence](../../develop/reference/osd/getsequence-method-in-class-sms_tasksequencepackage.md) method. GetSequence returns an [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object that you can change and then put back in the package by using the [SetSequence](../../develop/reference/osd/setsequence-method-in-class-sms_tasksequencepackage.md) method. For an example of using SetSequence, see [How to Create an Operating System Deployment Task Sequence Package](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-package.md).  

### To read a task sequence from a task sequence package  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Query the SMS Provider for the [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) that you want to load the sequence from.  

3.  Call the [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) class [GetSequence](../../develop/reference/osd/getsequence-method-in-class-sms_tasksequencepackage.md) method to get the [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object.  

4.  Make changes to the task sequence and put them back into the package by using [SetSequence](../../develop/reference/osd/setsequence-method-in-class-sms_tasksequencepackage.md).  

## Example  
 The following example method returns the task sequence object ([SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)) from the supplied package.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Function ReadTaskSequence(connection, taskSequencePackage)  
    ' Get the parameters object.  
    Set packageClass = connection.Get("SMS_TaskSequencePackage")  

    Set objInParam = packageClass.Methods_("GetSequence"). _  
        inParameters.SpawnInstance_()  

    ' Add the input parameters.  
     objInParam.Properties_.Item("TaskSequencePackage") =  taskSequencePackage  

    ' Get the sequence.  
     Set objOutParams = connection.ExecMethod("SMS_TaskSequencePackage", "GetSequence", objInParam)  
     Set ReadTaskSequence = objOutParams.TaskSequence  
End Function  
```  

```c#  
public IResultObject ReadTaskSequence(  
    WqlConnectionManager connection,   
    IResultObject taskSequencePackage)  
{  
    IResultObject taskSequence = null;  
    try  
    {  
        Dictionary<string, object> parameters = new Dictionary<string, object>();  
        parameters.Add("TaskSequencePackage", taskSequencePackage);  

        IResultObject outParams = connection.ExecuteMethod("SMS_TaskSequencePackage", "GetSequence", parameters);  
        taskSequence = outParams.GetSingleItem("TaskSequence");  

        return taskSequence;  
    }  
    catch (Exception e)  
    {  
        Console.WriteLine("failed to hydrate: " + e.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|-   A valid connection to the SMS Provider.|  

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
 [How to Create an Operating System Deployment Task Sequence Package](../../develop/osd/how-to-create-an-operating-system-deployment-task-sequence-package.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)   
 [How to Enumerate the Available Operating System Deployment Task Sequences](../../develop/osd/how-to-enumerate-the-available-operating-system-deployment-task-sequences.md)
