---
title: "Assign Configuration Baselines"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 54a9b910-2ed2-480c-adc8-aa61201ae39e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Assign Configuration Baselines
In System Center Configuration Manager, to assign a configuration baseline to a collection, an assignment instance is created, populated with a minimum set of required values, and saved.  

### To assign Configuration Baselines  

1.  Set up a connection to the SMS Provider.  

2.  Create an instance of `SMS_BaselineAssignment`.  

3.  Populate the instance properties.  

4.  Save the new `SMS_BaselineAssignment` instance.  

## Example  
 The following code examples show how to create an instance of a baseline assignment.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub DCMCreateAssignment(swbemServices,                     _  
                        baselineID,                        _  
                        applyToSubTargets,                 _  
                        assignmentAction,                  _  
                        assignmentName,                    _  
                        assignmentDescription,             _  
                        desiredConfigType,                 _  
                        distributionPointLocality,         _  
                        evaluationSchedule,                _  
                        logComplianceToWinEvent,           _  
                        notifyUser,                        _  
                        sendDetailedNonComplianceStatus,   _  
                        startTime,                         _  
                        suppressReboot,                    _  
                        targetCollectionID,                _  
                        useGMTTimes)  

' Create new assignment object.  
set newAssignment = swbemServices.Get("SMS_BaselineAssignment").SpawnInstance_()        

' Assign variable values to assignment properties.  
'    //  
'    // The following properties are set by the provider on put():  
'    //     AssignmentID  
'    //     AssignmentUniqueID  
'    //     SourceSite  
'    //     CreationTime  

newAssignment.ApplyToSubTargets = applyToSubTargets   
newAssignment.AssignmentAction = assignmentAction   
newAssignment.AssignmentName = assignmentName   
newAssignment.AssignmentDescription = assignmentDescription   
newAssignment.DesiredConfigType = desiredConfigType   
newAssignment.DPLocality = distributionPointLocality   
newAssignment.EvaluationSchedule = evaluationSchedule   
newAssignment.LogComplianceToWinEvent = logComplianceToWinEvent   
newAssignment.NotifyUser = notifyUser   
newAssignment.SendDetailedNonComplianceStatus = sendDetailedNonComplianceStatus   
newAssignment.StartTime = startTime   
newAssignment.SuppressReboot = suppressReboot   
newAssignment.TargetCollectionID = targetCollectionID   
newAssignment.UseGMTTimes = useGMTTimes   
newAssignment.AssignedCIs = Array(baselineID)   

' Save assignment.  
newAssignment.Put_  

Wscript.Echo " "  
Wscript.Echo "Created new assignment."      

End Sub  

```  

```c#  

public void DCMCreateAssignment(WqlConnectionManager connection,  
                                bool applyToSubTargets,  
                                int assignmentAction,  
                                string assignmentName,  
                                string assignmentDescription,  
                                string desiredConfigType,  
                                int distributionPointLocality,  
                                string evaluationSchedule,  
                                bool logComplianceToWinEvent,  
                                bool notifyUser,  
                                bool sendDetailedNonComplianceStatus,  
                                string startTime,  
                                int suppressReboot,  
                                string targetCollectionID,  
                                bool useGMTTimes,  
                                int baselineID)  
{  

    // Set required variables.   
    // Set AssignedCIs like array with a known baseline id (this is the initial creation of the assignment, so no existing values).  
    int[] arrayBaselineNumbers = new int[] { baselineID };  

    try  
    {  
        // Create new assignment object.  
        IResultObject newAssignment = connection.CreateInstance("SMS_BaselineAssignment");  

        // Assign variable values to assignment properties.  
        //  
        // The following properties are set by the provider on put():  
        //     AssignmentID  
        //     AssignmentUniqueID  
        //     SourceSite  
        //     CreationTime  
        newAssignment["ApplyToSubTargets"].BooleanValue = applyToSubTargets;  
        newAssignment["AssignmentAction"].IntegerValue = assignmentAction;  
        newAssignment["AssignmentName"].StringValue = assignmentName;  
        newAssignment["AssignmentDescription"].StringValue = assignmentDescription;  
        newAssignment["DesiredConfigType"].StringValue = desiredConfigType;  
        newAssignment["DPLocality"].IntegerValue = distributionPointLocality;  
        newAssignment["EvaluationSchedule"].StringValue = evaluationSchedule;  
        newAssignment["LogComplianceToWinEvent"].BooleanValue = logComplianceToWinEvent;  
        newAssignment["NotifyUser"].BooleanValue = notifyUser;  
        newAssignment["SendDetailedNonComplianceStatus"].BooleanValue = sendDetailedNonComplianceStatus;  
        newAssignment["StartTime"].StringValue = startTime;  
        newAssignment["SuppressReboot"].IntegerValue = suppressReboot;  
        newAssignment["TargetCollectionID"].StringValue = targetCollectionID;  
        newAssignment["AssignedCIs"].IntegerArrayValue = arrayBaselineNumbers;  
        newAssignment["UseGMTTimes"].BooleanValue = useGMTTimes;  

        // Save assignment object.  
        newAssignment.Put();  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create new assignment." + "\\n" + ex.Message);  
        throw;  
    }  

    Console.WriteLine("Created new assignment.");  

}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|-   `connection`<br />-   `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`applyToSubTargets`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` to apply the configuration item assignment to a subcollection.|  
|`assignmentAction`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Action associated with the configuration item assignment.|  
|`assignmentName`|-   Managed: `String`<br />-   VBScript: `String`|assignmentName|  
|`assignmentDescription`|-   Managed: `String`<br />-   VBScript: `String`|The local assignment name.|  
|`desiredConfigType`|-   Managed: `String`<br />-   VBScript: `String`|The type of the configuration item.|  
|`distributionPointLocality`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Flags that determine how the client obtains distribution points, according to distribution point locality.|  
|`evaluationSchedule`|-   Managed: `String`<br />-   VBScript: `String`|The assignment evaluation schedule.|  
|`logComplianceToWinEvent`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` to log compliance status to Windows event logs.|  
|`notifyUser`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` to notify the user when a configuration item is available.|  
|`sendDetailedNonComplianceStatus`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` to send a detailed non-compliance status message.|  
|`startTime`|-   Managed: `String`<br />-   VBScript: `String`|The date and time when the configuration item assignment was initially offered.|  
|`suppressReboot`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Value indicating whether the client should not reboot the computer, if there is a reboot pending after the configuration item is applied.|  
|`targetCollectionID`|-   Managed: `String`<br />-   VBScript: `String`|The identifier of the collection to which the assignment is targeted.|  
|`useGMTTimes`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|`true` if the times and schedules are in Universal Coordinated Time (UTC).|  
|`baselineID`|-   Managed: `Integer` Array<br />-   VBScript: `Integer` Array|Array of IDs for the configuration items targeted by the assignment.|  

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
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [About Configuration Baselines and Configuration Items](../../develop/compliance/about-configuration-baselines-and-configuration-items.md)   
 [How to Use Configuration Manager Objects With WMI](../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)   
 [SMS_BaselineAssignment Server WMI Class](../../develop/reference/compliance/sms_baselineassignment-server-wmi-class.md)
