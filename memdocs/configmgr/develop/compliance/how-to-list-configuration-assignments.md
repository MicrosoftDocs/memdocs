---
title: "List Configuration Assignments"
description: The following code examples show how to list the current configuration baseline assignments and a specific set of properties for each assignment in Configuration Manager.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: cd79bf83-591d-47b1-afdb-a23fbae90e58
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to List Configuration Assignments
The following code examples show how to list the current configuration baseline assignments and a specific set of properties for each assignment in Configuration Manager.  

### To list Configuration Assignments  

1.  Set up a connection to the SMS Provider.  

2.  Query for all instances `SMS_BaselineAssignment`.  

3.  Loop through the array of available configuration baseline assignments, listing each configuration baseline assignment and specific properties.  

## Example  
 The following example method shows how to list the current configuration baseline assignments and a specific set of properties for each assignment in Configuration Manager.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub DCMAssignments_ListProperties(swbemServices)  

    On Error Resume Next  

    Dim queryBaselineAssignmentResults  
    Dim assignment  

    ' Query assignments.  
    Set queryBaselineAssignmentResults = swbemServices.ExecQuery("Select * From SMS_BaselineAssignment", , 0)  

    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get assignments."  
        Exit Sub  
    End If  

    On Error Goto 0  

    ' List assignments and various assignment's properties.  
    For Each assignment In queryBaselineAssignmentResults  
        Wscript.Echo ""  
        Wscript.Echo "Listing Assignment Properties for Assignment ID: " & assignment.AssignmentID  
        Wscript.Echo "Listing Assignment Properties for Assignment Description: " & assignment.AssignmentDescription  
        Wscript.Echo "-------------------------------------------------------------------------------"  
        Wscript.Echo "ApplyToSubTargets: " & assignment.ApplyToSubTargets  
        Wscript.Echo "AssignmentAction:  " & assignment.AssignmentAction  
        Wscript.Echo "AssignmentID: " & assignment.AssignmentID  
        Wscript.Echo "AssignmentName: " & assignment.AssignmentName  
        Wscript.Echo "AssignmentDescription: " & assignment.AssignmentDescription  
        Wscript.Echo "AssignmentUniqueID: " & assignment.AssignmentUniqueID  
        Wscript.Echo "Collection: " & assignment.TargetCollectionID  
        Wscript.Echo "CreationTime: " & assignment.CreationTime  
        Wscript.Echo "DesiredConfigType: " & assignment.DesiredConfigType  
        Wscript.Echo "DPLocality: " & assignment.DPLocality  
        Wscript.Echo "EvaluationSchedule: " & assignment.EvaluationSchedule  
        Wscript.Echo "LogComplianceToWinEvent: " & assignment.LogComplianceToWinEvent  
        Wscript.Echo "NotifyUser: " & assignment.NotifyUser  
        Wscript.Echo "SendDetailedNonComplianceStatus: " & assignment.SendDetailedNonComplianceStatus  
        Wscript.Echo "SourceSite: " & assignment.SourceSite  
        Wscript.Echo "StartTime: " & assignment.StartTime  
        Wscript.Echo "SuppressReboot: " & assignment.SuppressReboot  
        Wscript.Echo "UseGMTTimes: " & assignment.UseGMTTimes  
        Wscript.Echo "==============================================================================="  
    Next  

    If queryBaselineAssignmentResults.Count = 0 Then  
        Wscript.Echo "      no query results"  
    End If  

    set queryBaselineAssignmentResults = Nothing  

End Sub  

```  

```c#  

public void DCMAssignments_ListProperties(WqlConnectionManager connection)  
{  

    IResultObject baselineAssignments = connection.QueryProcessor.ExecuteQuery("SELECT * FROM SMS_BaselineAssignment");  

    try  
    {  
        foreach (IResultObject assignment in baselineAssignments)  
        {  
            Console.WriteLine("Listing Assignment Properties for Assignment ID: " + assignment["AssignmentID"].StringValue);  
            Console.WriteLine("Listing Assignment Properties for Assignment Description: " + assignment["AssignmentDescription"].StringValue);  
            Console.WriteLine("--------------------------------------------------------------------------------");  
            Console.WriteLine("ApplyToSubTargets: " + assignment["ApplyToSubTargets"].BooleanValue);  
            Console.WriteLine("AssignmentAction:  " + assignment["AssignmentAction"].IntegerValue);  
            Console.WriteLine("AssignmentID: " + assignment["AssignmentID"].StringValue);  
            Console.WriteLine("AssignmentName: " + assignment["AssignmentName"].StringValue);  
            Console.WriteLine("AssignmentDescription: " + assignment["AssignmentDescription"].StringValue);  
            Console.WriteLine("AssignmentUniqueID: " + assignment["AssignmentUniqueID"].StringValue);  
            Console.WriteLine("Collection: " + assignment["TargetCollectionID"].StringValue);  
            Console.WriteLine("CreationTime: " + assignment["CreationTime"].StringValue);  
            Console.WriteLine("DesiredConfigType: " + assignment["DesiredConfigType"].StringValue);  
            Console.WriteLine("DPLocality: " + assignment["DPLocality"].IntegerValue);  
            Console.WriteLine("EvaluationSchedule: " + assignment["EvaluationSchedule"].StringValue);  
            Console.WriteLine("LogComplianceToWinEvent: " + assignment["LogComplianceToWinEvent"].BooleanValue);  
            Console.WriteLine("NotifyUser: " + assignment["NotifyUser"].BooleanValue);  
            Console.WriteLine("SendDetailedNonComplianceStatus: " + assignment["SendDetailedNonComplianceStatus"].BooleanValue);  
            Console.WriteLine("SourceSite: " + assignment["SourceSite"].StringValue);  
            Console.WriteLine("StartTime: " + assignment["StartTime"].StringValue);  
            Console.WriteLine("SuppressReboot: " + assignment["SuppressReboot"].IntegerValue);  
            Console.WriteLine("UseGMTTimes: " + assignment["UseGMTTimes"].BooleanValue);  

            // Process the array.  
            int[] arrayofAssignedCIs = assignment["AssignedCIs"].IntegerArrayValue;  
            Console.Write("Assigned baseline ID(s): ");  
            foreach (int i in arrayofAssignedCIs)  
            {  
                Console.Write(i + " ");  
            }  

            Console.WriteLine();  

            // NULL BY DEFAULT (on a generic assignment created through the user interface).  
            //  
            //Console.WriteLine("EnforcementDeadline: " + assignment["EnforcementDeadline"].StringValue);  
            //Console.WriteLine("ExpirationTime: " + assignment["ExpirationTime"].StringValue);  
            //Console.WriteLine("NonComplianceCriticality: " + assignment["NonComplianceCriticality"].IntegerValue);  
            //Console.WriteLine("OverrideServiceWindows: " + assignment["OverrideServiceWindows"].BooleanValue);  
            //Console.WriteLine("RebootOutsideOfServiceWindows: " + assignment["RebootOutsideOfServiceWindows"].BooleanValue);  
            //Console.WriteLine("WoLEnabled: " + assignment["WoLEnabled"].BooleanValue);  

            Console.WriteLine("================================================================================");  

        }  

    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to list assignment properties. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|-   `connection`<br />-   `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  

## Compiling the Code  

### Namespaces  
 System  

 System.Collections.Generic  

 System.ComponentModel  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About Configuration Baselines and Configuration Items](../../develop/compliance/about-configuration-baselines-and-configuration-items.md)   
 [Objects overview](../core/understand/configuration-manager-objects-overview.md)
 [How to Connect to a Configuration Manager Provider using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_BaselineAssignment Server WMI Class](../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)
