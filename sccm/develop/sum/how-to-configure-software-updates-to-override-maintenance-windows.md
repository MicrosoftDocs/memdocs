---
title: "Configure Software Updates to Override Maintenance Windows"
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
ms.assetid: 2b623f07-91ab-43cf-999c-7f868855eb3asearchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Configure Software Updates to Override Maintenance Windows
You configure software updates to override maintenance windows, in System Center Configuration Manager, by updating the `OverrideServiceWindows` property of an assignment (deployment).  

### To configure software updates to override maintenance windows  

1.  Set up a connection to the SMS Provider.  

2.  Load the specific assignment (deployment) to modify using the `SMS_UpdatesAssignment` class.  

3.  Set the `OverrideServiceWindows` value to `true`.  

4.  Save the assignment (deployment) and properties.  

## Example  
 The following example method shows how to configure software updates to override maintenance windows by using the `SMS_UpdatesAssignment` class and class properties.  

> [!NOTE]
>  This task only applies to mandatory deployments.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureSoftwareUpdatestoOverrideMaintenanceWindow(connection, existingAssignmentID)  

    ' Get the specific SMS_UpdatesAssignment instance to modify.   
    Set assignmentToModify = connection.Get("SMS_UpdatesAssignment.AssignmentID=" & existingAssignmentID & "")    

    ' Set the new property value.  
    assignmentToModify.OverrideServiceWindows = true  

    ' Save the assignment.  
    assignmentToModify.Put_   

    ' Output the new property values.  
    Wscript.Echo " "  
    Wscript.Echo "Set assignment " & existingAssignmentID & " to override service windows."  

End Sub  

```  

```c#  

public void ConfigureSoftwareUpdatestoOverrideMaintenanceWindow(WqlConnectionManager connection, int existingAssignmentID)  
{  
    try  
    {  
        // Get the specific SMS_UpdatesAssignment instance to change.  
        IResultObject updatesAssignmentToChange = connection.GetInstance(@"SMS_UpdatesAssignment.AssignmentID=" + existingAssignmentID);  

        // Set OverrideServiceWindows property.  
        updatesAssignmentToChange["OverrideServiceWindows"].BooleanValue = true;  

        // Save property changes.  
        updatesAssignmentToChange.Put();  

        // Output success message.  
        Console.WriteLine("Set assignment " + existingAssignmentID + " to override service windows.");  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to .... Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`existingAssignmentID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|An existing Assignment ID to modify.|  

## Compiling the Code  
 This C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.Text  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Software Updates](../../develop/sum/software-updates.md)   
 [Software Updates and Maintenance Windows](../../develop/sum/software-updates-and-maintenance-windows.md)   
 [SMS_UpdatesAssignment](../../develop/reference/sum/sms_updatesassignment-server-wmi-class.md)
