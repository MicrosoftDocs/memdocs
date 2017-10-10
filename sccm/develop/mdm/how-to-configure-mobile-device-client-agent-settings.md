---
title: "Configure Mobile Device Client Agent Settings"
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
ms.assetid: bb2e1e0a-095f-4b7d-92ba-29a89c8d8f69searchScope: - ConfigMgr SDK
caps.latest.revision: 16
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Configure Mobile Device Client Agent Settings
You configure the Mobile Device Client Agent settings, in System Center Configuration Manager, by modifying the site control file.  

> [!IMPORTANT]
>  This topic only applies to the Mobile Device Legacy Client. For addition information on the Mobile Device Legacy Client platforms, see the Mobile Device Legacy Client section of the [Supported Configurations for Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=272885).  

### To configure the Mobile Device Client Agent settings  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Device Client section of the site control file by using the `SMS_SCI_ClientComp` class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the property changes to the site control file.  

## Example  
 The following example method configures various Mobile Device Client Agent settings by using the `SMS_SCI_ClientComp` class to connect to the site control file and change properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureMobileDeviceClientAgentSettings(swbemServices,                        _  
                                             swbemContext,                         _  
                                             siteCode,                             _  
                                             newPollIntervalMinutes,               _  
                                             newPollIntervalHours,                 _  
                                             newFailureRetryCount,                 _  
                                             newFailureRetryIntervalMinutes,       _   
                                             newFailureRetryIntervalHours,         _  
                                             newEnableDisableSoftwareDistribution)  

    ' Variables to build poll interval string.  
    ' Note: The sample code only passes in minutes and hours, so setting empty values to use.  
    emptySeconds = "00"  
    emptyDays = "00"  
    emptyMonths = "00"  
    emptyYears = "0000"  

    ' Build newPollInterval string (the format must be "0000-00-00 00:00:00").  
    newPollInterval = emptyYears & "-" & emptyMonths & "-" & emptyDays & " " & newPollIntervalHours & ":" & newPollIntervalMinutes & ":" & emptySeconds  
    newFailureRetryInterval = emptyYears & "-" & emptyMonths & "-" & emptyDays & " " & newFailureRetryIntervalHours & ":" & newFailureRetryIntervalMinutes & ":" & emptySeconds  

    ' Load site control file and get the client component section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_ClientComp " & _  
    "WHERE ClientComponentName = 'Device Client' " & _  
    "AND SiteCode = '" & siteCode & "'"            

    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Loop through the array of embedded property instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Poll Interval  
            If vProperty.PropertyName = "Poll Interval" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value2                 

                'Modify the value.  
                vProperty.Value2 = newPollInterval  
                wscript.echo "New value " & newPollInterval  
            End If  

            ' Setting: Failure Retry Count  
            If vProperty.PropertyName = "Failure Retry Count" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newFailureRetryCount  
                wscript.echo "New value " & newFailureRetryCount  
            End If  

            ' Setting: Failure Retry Interval  
            If vProperty.PropertyName = "Failure Retry Interval" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value2                 

                ' Modify the value.  
                vProperty.Value2 = newFailureRetryInterval  
                wscript.echo "New value " & newFailureRetryInterval  
            End If  

            ' Setting: Enable Software Dist  
            If vProperty.PropertyName = "Enable Software Dist" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value2                 

                ' Modify the value.  
                vProperty.Value2 = newEnableDisableSoftwareDistribution  
                wscript.echo "New value " & newEnableDisableSoftwareDistribution  
            End If  

        Next     

        ' Update the component in your copy of the site control file. Get the path  
        ' to the updated object, which could be used later to retrieve the instance.  
        Set SCICompPath = SCIComponent.Put_(wbemChangeFlagUpdateOnly, swbemContext)  

    Next  

    ' Commit the change to the actual site control file.  
    Set InParams = swbemServices.Get("SMS_SiteControlFile").Methods_("CommitSCF").InParameters.SpawnInstance_  
    InParams.SiteCode = siteCode  
    swbemServices.ExecMethod "SMS_SiteControlFile", "CommitSCF", InParams, , swbemContext  

End Sub  

```  

```c#  

public void ConfigureMobileDeviceClientAgentSettings(WqlConnectionManager connection,  
                                                     string siteCode,  
                                                     string newPollIntervalMinutes,  
                                                     string newPollIntervalHours,  
                                                     string newFailureRetryCount,  
                                                     string newFailureRetryIntervalMinutes,  
                                                     string newFailureRetryIntervalHours,  
                                                     bool newEnableDisableSoftwareDistribution)  
{  

    // Define variables to build poll interval string.  
    // Note: The example code only passes in minutes and hours, so this sets empty values to use.  
    string emptyDays = "00";  
    string emptyMonths = "00";  
    string emptyYears = "0000";  
    string emptySeconds = "00";  

    // Build newPollInterval and newFailureRetryInterval strings (the format must be "0000-00-00 00:00:00").  
    string newPollInterval = emptyYears + "-" + emptyMonths + "-" + emptyDays + " " + newPollIntervalHours + ":" + newPollIntervalMinutes + ":" + emptySeconds;  
    string newFailureRetryInterval = emptyYears + "-" + emptyMonths + "-" + emptyDays + " " + newFailureRetryIntervalHours + ":" + newFailureRetryIntervalMinutes + ":" + emptySeconds;  

    try  
    {  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Device Client'");  

        // Loop through the array of embedded properties.  
        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Create temporary working copy of embedded properties.  
            Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

            // Setting: Poll Interval.  
            if (kvp.Value.PropertyList["PropertyName"] == "Poll Interval")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value2"].StringValue);  

                // Change value using the newPollInterval value passed in.   
                embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value2"].StringValue = newPollInterval;  
                Console.WriteLine("New value    : " + newPollInterval);  
            }  

            // Setting: Failure Retry Count.  
            if (kvp.Value.PropertyList["PropertyName"] == "Failure Retry Count")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value"].StringValue);  

                // Change value using the newFailureRetryCount value passed in.   
                embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value"].StringValue = newFailureRetryCount;  
                Console.WriteLine("New value    : " + newFailureRetryCount);  
            }  

            // Setting: Failure Retry Interval.  
            if (kvp.Value.PropertyList["PropertyName"] == "Failure Retry Interval")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value2"].StringValue);  

                // Change value using the newFailureRetryInterval value passed in.   
                embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value2"].StringValue = newFailureRetryInterval;  
                Console.WriteLine("New value    : " + newFailureRetryInterval);  
            }  

            // Setting: Enable Software Dist.  
            if (kvp.Value.PropertyList["PropertyName"] == "Enable Software Dist")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value2"].StringValue);  

                // Change value using the newEnableDisableSoftwareDistribution value passed in.   
                embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value2"].BooleanValue = newEnableDisableSoftwareDistribution;  
                Console.WriteLine("New value    : " + newEnableDisableSoftwareDistribution);  
            }  

            // Store the settings that have changed.  
            siteDefinition.EmbeddedProperties = embeddedProperties;  
        }  

        // Save the settings.   
        siteDefinition.Put();  

    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);  
        throw;  
    }  
}  

```  

 The example method has the following parameters:  

||||  
|-|-|-|  
|Parameter|Type|Description|  
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`newPollInterval`|-   Managed: `String`<br />-   VBScript: `String`|The interval that the client tries to contact the server.<br /><br /> The format of the string must be:<br /><br /> Years-months-days hours:minutes:seconds<br /><br /> "0000-00-00 00:00:00"|  
|`newPollIntervalMinutes`|-   Managed: `String`<br />-   VBScript: `String`|A value representing the minutes of the `newPollInterval` string.|  
|`newPollIntervalHours`|-   Managed: `String`<br />-   VBScript: `String`|A value representing the hours of the `newPollInterval` string.|  
|`newFailureRetryCount`|-   Managed: `String`<br />-   VBScript: `String`|A value representing the hours of the `newPollInterval` string.|  
|`newFailureRetryIntervalMinutes`|-   Managed: `String`<br />-   VBScript: `String`|A value representing the minutes of the `newFailureRetryInterval` string.|  
|`newFailureRetryIntervalHours`|-   Managed: `String`<br />-   VBScript: `String`|A value representing the hours of the `newFailureInterval` string.|  
|`newEnableDisableSoftwareDistribution`|-   Managed: `Boolean`<br />-   VBScript: `Boolean`|A value that enables or disables software distribution.<br /><br /> Enabled = `true`<br /><br /> Disabled = `false`|  

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
 [Configuration Manager SDK](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Mobile Device Management](../../develop/mdm/mobile-device-management.md)   
 [About Software Updates Setup and Configuration](../../develop/sum/about-software-updates-setup-and-configuration.md)   
 [About the Configuration Manager Site Control File](../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
