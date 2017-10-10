---
title: "Enumerate the Available OS Deployment Task Sequences"
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
ms.assetid: 0ea07b95-7474-4294-8c17-37e7a9e6957asearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Enumerate the Available Operating System Deployment Task Sequences
You enumerate the available operating system deployment task sequences, in System Center Configuration Manager, by querying the available task sequence packages. System Center Configuration Manager does not maintain instances of the [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) class for task sequences, but there is one instance of the [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md) class for each task sequence.  

> [!NOTE]
>  Several properties are lazy and you must get the object instance before you can access the properties.  

 You can also access individual task sequence packages by using the [PackageID](../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) key property. For an example, see [How to Read a Configuration Manager Object by Using Managed Code](../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md). After you have the task sequence package, you must create an [SMS_TaskSequence](../../develop/reference/osd/sms_tasksequence-server-wmi-class.md) object for the task sequence before you can change it. For more information, see [How to Read a Task Sequence From a Task Sequence Package](../../develop/osd/how-to-read-a-task-sequence-from-a-task-sequence-package.md).  

### To enumerate the available task sequence packages  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Query the SMS Provider for the available instances of [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md).  

3.  Display the required properties for each task sequence package returned by the query.  

## Example  
 The following example method queries the SMS Provider for the available instance of [SMS_TaskSequencePackage](../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md). To retrieve the lazy properties, the example gets the entire object from the SMS Provider.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub EnumerateTaskSequencePackages(connection)  

    Set taskSequencePackages= connection.ExecQuery("Select * from SMS_TaskSequencePackage")  

    For Each package in taskSequencePackages  
        WScript.Echo package.Name  
        WScript.Echo package.Sequence  
    Next  
End Sub  
```  

```c#  
public void EnumerateTaskSequencePackages(  
    WqlConnectionManager connection)  
{  
    IResultObject taskSequencePackages = connection.QueryProcessor.ExecuteQuery("select * from SMS_TaskSequencePackage");  

    foreach (IResultObject ro in taskSequencePackages)  
    {  
        ro.Get();  

        // Get the lazy properties - Sequence property contains the Task sequence XML.  
        Console.WriteLine(ro["Name"].StringValue);  
        Console.WriteLine(ro["Sequence"].StringValue);  

        Console.WriteLine();  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  

## Compiling the Code  
 The C# example requires:  

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
 [How to Read a Task Sequence From a Task Sequence Package](../../develop/osd/how-to-read-a-task-sequence-from-a-task-sequence-package.md)   
 [Operating System Deployment Task Sequencing](../../develop/osd/operating-system-deployment-task-sequencing.md)
