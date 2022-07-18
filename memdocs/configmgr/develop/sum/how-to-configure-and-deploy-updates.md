---
title: "Configure and Deploy Updates"
titleSuffix: "Configuration Manager"
description: Learn how to use the Configuration Manager SDK to configure and deploy software updates
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: bd5be2ec-0db9-4bdb-adc6-452c2103b5b4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Configure and Deploy Updates
You create a software updates deployment, in Configuration Manager, by creating an instance of the [SMS_UpdatesAssignment Server WMI Class](../../develop/reference/sum/sms_updatesassignment-server-wmi-class.md) and populating the properties.  

### To configure and deploy updates  

1.  Set up a connection to the SMS Provider.  

2.  Create the new deployment object by using the [SMS_UpdatesAssignment](../../develop/reference/sum/sms_updatesassignment-server-wmi-class.md) class.  

3.  Populate the new deployment properties.  

4.  Save the new deployment and properties.  

## Example  
 The following example method shows how to create a software updates deployment by using the [SMS_UpdatesAssignment](../../develop/reference/sum/sms_updatesassignment-server-wmi-class.md) class. Note that the parameters of the example method reflect certain properties of `SMS_UpdatesAssignment`.  

> [!IMPORTANT]
>  The methods below require an array of the assigned configuration items (CI_IDs). The update content for these CI_IDs must have already been downloaded and added to an updates deployment package.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureAndDeploySUMUpdates(connection,                             _  
                                  newApplyToSubTargets,                  _  
                                  newArrayAssignedCIs,                   _  
                                  newAssignmentAction,                   _  
                                  newAssignmentDescription,              _  
                                  newAssignmentName,                     _  
                                  newDesiredConfigType,                  _  
                                  newDPLocality,                         _   
                                  newLocaleID,                           _  
                                  newLogComplianceToWinEvent,            _  
                                  newNotifyUser,                         _  
                                  newRaiseMomAlertsOnFailure,            _  
                                  newSendDetailedNonComplianceStatus,    _  
                                  newStartTime,                          _  
                                  newSuppressReboot,                     _  
                                  newTargetCollectionID,                 _  
                                  newUseGMTTimes)  

  ' Create the new deployment object.  
  Set newSUMUpdatesAssignment = connection.Get("SMS_UpdatesAssignment").SpawnInstance_  

  ' Populate the deployment properties.  
  newSUMUpdatesAssignment.ApplyToSubTargets = newApplyToSubTargets  
  newSUMUpdatesAssignment.AssignedCIs = newArrayAssignedCIs  
  newSUMUpdatesAssignment.AssignmentAction = newAssignmentAction  
  newSUMUpdatesAssignment.AssignmentDescription = newAssignmentDescription  
  newSUMUpdatesAssignment.AssignmentName = newAssignmentName  
  newSUMUpdatesAssignment.DesiredConfigType = newDesiredConfigType  
  newSUMUpdatesAssignment.DPLocality = newDPLocality  
  newSUMUpdatesAssignment.LocaleID = newLocaleID  
  newSUMUpdatesAssignment.LogComplianceToWinEvent = newLogComplianceToWinEvent  
  newSUMUpdatesAssignment.NotifyUser = newNotifyUser  
  newSUMUpdatesAssignment.RaiseMomAlertsOnFailure = newRaiseMomAlertsOnFailure  
  newSUMUpdatesAssignment.SendDetailedNonComplianceStatus = newSendDetailedNonComplianceStatus  
  newSUMUpdatesAssignment.StartTime = newStartTime  
  newSUMUpdatesAssignment.SuppressReboot = newSuppressReboot  
  newSUMUpdatesAssignment.TargetCollectionID = newTargetCollectionID  
  newSUMUpdatesAssignment.UseGMTTimes = newUseGMTTimes  

  ' Save the new deployment and properties.  
  newSUMUpdatesAssignment.Put_   

  ' Output the new deployment name.  
  Wscript.Echo "Created new deployment " & newSUMUpdatesAssignment.AssignmentName                    

End Sub  

```  

```c#  

public void ConfigureAndDeploySUMUpdates(WqlConnectionManager connection,  
                                        bool newApplyToSubTargets,  
                                        int[] newArrayAssignedCIs,  
                                        int newAssignmentAction,  
                                        string newAssignmentDescription,  
                                        string newAssignmentName,  
                                        int newDesiredConfigType,  
                                        int newDPLocality,  
                                        int newLocaleID,  
                                        bool newLogComplianceToWinEvent,  
                                        bool newNotifyUser,  
                                        bool newRaiseMomAlertsOnFailure,  
                                        bool newSendDetailedNonComplianceStatus,  
                                        string newStartTime,  
                                        int newSuppressReboot,  
                                        string newTargetCollectionID,  
                                        bool newUseGMTTimes)      
{  
    try  
    {  

        // Create the deployment object.  
        IResultObject newSUMUpdatesAssignment = connection.CreateInstance("SMS_UpdatesAssignment");  

        // Populate new deployment properties.  
        // Note: newTemplateName must be unique.  

        newSUMUpdatesAssignment["ApplyToSubTargets"].BooleanValue = newApplyToSubTargets;  
        newSUMUpdatesAssignment["AssignedCIs"].IntegerArrayValue = newArrayAssignedCIs;  
        newSUMUpdatesAssignment["AssignmentAction"].IntegerValue = newAssignmentAction;  
        newSUMUpdatesAssignment["AssignmentDescription"].StringValue = newAssignmentDescription;         
        newSUMUpdatesAssignment["AssignmentName"].StringValue = newAssignmentName;  
        newSUMUpdatesAssignment["DesiredConfigType"].IntegerValue = newDesiredConfigType;  
        newSUMUpdatesAssignment["DPLocality"].IntegerValue = newDPLocality;  
        newSUMUpdatesAssignment["LocaleID"].IntegerValue = newLocaleID;  
        newSUMUpdatesAssignment["LogComplianceToWinEvent"].BooleanValue = newLogComplianceToWinEvent;  
        newSUMUpdatesAssignment["NotifyUser"].BooleanValue = newNotifyUser;  
        newSUMUpdatesAssignment["RaiseMomAlertsOnFailure"].BooleanValue = newRaiseMomAlertsOnFailure;  
        newSUMUpdatesAssignment["SendDetailedNonComplianceStatus"].BooleanValue = newSendDetailedNonComplianceStatus;  
        newSUMUpdatesAssignment["StartTime"].DateTimeValue = newStartTime;  
        newSUMUpdatesAssignment["SuppressReboot"].IntegerValue = newSuppressReboot;  
        newSUMUpdatesAssignment["TargetCollectionID"].StringValue = newTargetCollectionID;  
        newSUMUpdatesAssignment["UseGMTTimes"].BooleanValue = newUseGMTTimes;  

        // Save new deployment and new deployment properties.  
        newSUMUpdatesAssignment.Put();  

        // Output the new deployment name.  
        Console.WriteLine("Created deployment: " + newAssignmentName);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create newSUMUpdatesAssignment. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

|Parameter|Type|Description|
|---------|----|-----------|
|`Connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`newApplyToSubTargets`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Determines whether the deployment applies to subtargets.<br /><br /> -   True<br />-   False|  
|`newArrayAssignedCIs`|-   Managed: `Integer` array<br />-   VBScript: `Integer` array|An array of the assigned configuration items (CI_IDs). The update content for these CI_IDs must have already been downloaded and added to an updates deployment package.|  
|`newAssignmentAction`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The new assignment action.|  
|`newAssignmentDescription`|-   Managed: `String`<br />-   VBScript: `String`|The new assignment description.|  
|`newAssignmentName`|-   Managed: `String`<br />-   VBScript: `String`|The new assignment name.|  
|`newDesiredConfigType`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The new desired configuration type.|  
|`newDPLocality`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The new distribution point locality.|  
|`newLocaleID`|-   Managed: `Integer`<br />-   VBScript: `Integer`|The new locale ID.|  
|`newLogComplianceToWinEvent`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Determines whether compliance is logged to the Windows Event log.<br /><br /> -   True<br />-   False|  
|`newNotifyUser`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Identifies whether users are notified.<br /><br /> -   True<br />-   False|  
|`newRaiseMomAlertsOnFailure`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Identifies whether MOM alerts are raised on failure.<br /><br /> -   True<br />-   False|  
|`newSendDetailedNonComplianceStatus`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Identifies whether detailed noncompliance status is sent.<br /><br /> -   True<br />-   False|  
|`newStartTime`|-   Managed: `String`<br />-   VBScript: `String`|The new start time.|  
|`newSuppressReboot`|-   Managed: `Integer`<br />-   VBScript: `Integer`|Identifies whether reboot is suppressed.|  
|`newTargetCollectionID`|-   Managed: `String`<br />-   VBScript: `String`|The new target collection IDs.|  
|`newUseGMTTimes`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|Identifies whether to use Coordinated Universal Time (UTC).<br /><br /> -   True<br />-   False|  

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
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../develop/core/servers/configure/role-based-administration.md).  

## See also

[About software update deployments](about-software-updates-deployments.md)

[SMS_UpdatesAssignment](../reference/sum/sms_updatesassignment-server-wmi-class.md)
