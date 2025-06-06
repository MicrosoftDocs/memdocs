---
description: Learn how to configure software distribution advertised programs client agent settings in the site control file.
title: Configure Advertised Programs Client Agent Settings
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 5a5ffe1b-6e82-480f-97e8-2840ba704170
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart
---
# How to Configure Software Distribution Advertised Programs Client Agent Settings
In Configuration Manager, the site control file maintains configuration for the configuration of the site. This topic shows how to configure software distribution advertised programs client agent settings in the site control file. For more information about reading from and writing to the site control file, see [About the site control file](../../understand/about-the-configuration-manager-site-control-file.md).

> [!CAUTION]
>  You should be experienced in managing a site's configuration before using the SMS Provider classes to modify the site configuration. You should use caution or avoid using the `SMS_SCI_FileDefinition` and `SMS_SCI_SiteDefinition` classes altogether. These classes manage the site control file itself. You can cause significant damage to a site by changing some configurable items.

### To configure client agent settings

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../../understand/sms-provider-fundamentals.md).

2.  Make a connection to the software distribution client component section of the site control file by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class.

3.  Loop through the array of available properties, making changes as needed.

4.  Commit the property changes to the site control file.

## Example
 The following example queries for specific items in the software distribution client component section of the site control file, and modifies those specific client agent settings.

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).

```vbs

Sub ConfigureClientAgentSettings(swbemServices, swbemContext, siteToChange, enableDisableSWDClientAgent, enableDisableRequestUserPolicy, setPolicyRefreshInterval, enableDisableVisibleSignalOnAvailable, enableDisableAudibleSignalonAvailable,enableDisableCountdownSignal,setCountdownMinutes, enableDisableShowIcon)

    ' Load site control file and get SWD client component section.
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteToChange & """", "Refresh", , , swbemContext
    Set objSWbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteToChange & "',ItemName='Software Distribution'", , swbemContext)

    ' Display SWD client agent settings before change.
    Wscript.Echo " "
    Wscript.Echo "Before Change"
    Wscript.Echo "-------------"

    Wscript.Echo " "
    Wscript.Echo objSWbemInst.ClientComponentName
    Wscript.Echo "Current value: " & objSWbemInst.Flags & " (0 = Disabled, 1 = Enabled)"
    Wscript.Echo " "
    objSWbemInst.Flags = enableDisableSWDClientAgent

    ' Enumerate though the property array, but display only the properties that we're specifically interested in.
    ' Note: A list of all properties could be generated by just using the following code:
    '     PropertyArray = objSwbemInst.props
    '     For i = 0 to ubound(PropertyArray)
    '        Wscript.Echo PropertyArray(i).PropertyName
    '        Wscript.Echo "Current value: " & PropertyArray(i).Value
    '     Next

    PropertyArray = objSwbemInst.props
    For i = 0 to ubound(PropertyArray)

        ' Client settings: Allow user targeted advertisement requests.
        If PropertyArray(i).PropertyName = "Request User Policy" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
            PropertyArray(i).Value = enableDisableRequestUserPolicy
        End If

        ' Client settings: Policy polling interval (minutes).
        If PropertyArray(i).PropertyName = "Policy Refresh Interval" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
            PropertyArray(i).Value = setPolicyRefreshInterval
        End If

        ' When new advertised programs are available: Display a notification message.
        If PropertyArray(i).PropertyName = "Visible Signal on Available" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
            PropertyArray(i).Value = enableDisableVisibleSignalOnAvailable
        End If

        ' When new advertised programs are available: Play a sound.
        If PropertyArray(i).PropertyName = "Audible Signal on Available" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
            PropertyArray(i).Value = enableDisableAudibleSignalonAvailable
        End If

        ' When a scheduled program is about to run: Provide a countdown.
        If PropertyArray(i).PropertyName = "Countdown Signal" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
            PropertyArray(i).Value = enableDisableCountdownSignal
        End If

        ' Countdown length (minutes).
        If PropertyArray(i).PropertyName = "Countdown Minutes" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
            PropertyArray(i).Value = setCountdownMinutes
        End If

        ' Show advertised program notification icons in the notification area.
        If PropertyArray(i).PropertyName = "Show Icon" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
            PropertyArray(i).Value = enableDisableShowIcon
        End If
    Next

    ' Save new client agent settings.
    objSWbemInst.Put_ , swbemContext
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteToChange & """", "Commit", , , swbemContext

    ' Refresh in-memory copy of the site control file and get the SWD client component section.
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteToChange & """", "Refresh", , , swbemContext
    Set objSWbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteToChange & "',ItemName='Software Distribution'", , swbemContext)

    ' Display SWD client agent settings after change.

    Wscript.Echo " "
    Wscript.Echo "After Change"
    Wscript.Echo "------------"

    Wscript.Echo " "
    Wscript.Echo objSWbemInst.ClientComponentName
    Wscript.Echo "Current value: " & objSWbemInst.Flags & " (0 = Disabled, 1 = Enabled)"
    Wscript.Echo " "

    PropertyArray = objSwbemInst.props
    For i = 0 to ubound(PropertyArray)

        ' Client settings: Allow user targeted advertisement requests.
        If PropertyArray(i).PropertyName = "Request User Policy" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
        End If

        ' Client settings: Policy polling interval (minutes).
        If PropertyArray(i).PropertyName = "Policy Refresh Interval" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
        End If

        ' When new advertised programs are available: Display a notification message.
        If PropertyArray(i).PropertyName = "Visible Signal on Available" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
        End If

        ' When new advertised programs are available: Play a sound.
        If PropertyArray(i).PropertyName = "Audible Signal on Available" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
        End If

        ' When a scheduled program is about to run: Provide a countdown.
        If PropertyArray(i).PropertyName = "Countdown Signal" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
        End If

        ' Countdown length (minutes).
        If PropertyArray(i).PropertyName = "Countdown Minutes" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
        End If

        ' Show advertised program notification icons in the notification area.
        If PropertyArray(i).PropertyName = "Show Icon" Then
            Wscript.Echo PropertyArray(i).PropertyName
            Wscript.Echo "Current value: " & PropertyArray(i).Value
            Wscript.Echo " "
        End If
    Next

End Sub
```

```c#
public void ConfigureSWDClientAgentSettings(WqlConnectionManager connection, string siteCode, string enableDisableSWDClientAgent, string enableDisableRequestUserPolicy, string setPolicyRefreshInterval, string enableDisableVisibleSignalOnAvailable, string enableDisableAudibleSignalonAvailable, string enableDisableCountdownSignal, string setCountdownMinutes, string enableDisableShowIcon)
{
try
{
    IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Software Distribution'");

    Console.WriteLine();
    Console.WriteLine("Before Change");
    Console.WriteLine("-------------");

    // Enable software distribution to clients.
    // Set SWD client agent by setting flags value to  0 or 1 using the EnableDisableSWDClientAgent variable.
    Console.WriteLine("Software Distribution Client Agent");
    Console.WriteLine("Current value: " + siteDefinition["Flags"].StringValue + " (0 = Disabled, 1 = Enabled)");
    siteDefinition["Flags"].StringValue = enableDisableSWDClientAgent;

    foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)
    {
        Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties; // temp copy

        // Client settings: Allow user targeted advertisement requests.
        if (kvp.Value.PropertyList["PropertyName"] == "Request User Policy")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Request User Policy"]["Value"].StringValue);
            embeddedProperties["Request User Policy"]["Value"].StringValue = enableDisableRequestUserPolicy;
        }

        // Client settings: Policy polling interval (minutes).
        if (kvp.Value.PropertyList["PropertyName"] == "Policy Refresh Interval")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Policy Refresh Interval"]["Value"].StringValue);
            embeddedProperties["Policy Refresh Interval"]["Value"].StringValue = setPolicyRefreshInterval;
        }

        // When new advertised programs are available: Display a notification message.
        if (kvp.Value.PropertyList["PropertyName"] == "Visible Signal on Available")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Visible Signal on Available"]["Value"].StringValue);
            embeddedProperties["Visible Signal on Available"]["Value"].StringValue = enableDisableVisibleSignalOnAvailable;
        }

        // When new advertised programs are available: Play a sound.
        if (kvp.Value.PropertyList["PropertyName"] == "Audible Signal on Available")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Audible Signal on Available"]["Value"].StringValue);
            embeddedProperties["Audible Signal on Available"]["Value"].StringValue = enableDisableAudibleSignalonAvailable;
        }

        // When a scheduled program is about to run: Provide a countdown.
        if (kvp.Value.PropertyList["PropertyName"] == "Countdown Signal")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Countdown Signal"]["Value"].StringValue);
            embeddedProperties["Countdown Signal"]["Value"].StringValue = enableDisableCountdownSignal;
        }

        // Countdown length (minutes).
        if (kvp.Value.PropertyList["PropertyName"] == "Countdown Minutes")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Countdown Minutes"]["Value"].StringValue);
            embeddedProperties["Countdown Minutes"]["Value"].StringValue = setCountdownMinutes;
        }

        // Show advertised program notification icons in the notification area.
        if (kvp.Value.PropertyList["PropertyName"] == "Show Icon")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Show Icon"]["Value"].StringValue);
            embeddedProperties["Show Icon"]["Value"].StringValue = enableDisableShowIcon;
        }

        // Store the settings that have changed.
        siteDefinition.EmbeddedProperties = embeddedProperties;
    }

    // Save the settings.
    siteDefinition.Put();

    // Verify change by reconnecting and getting the value again.
    IResultObject siteDefinition2 = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Software Distribution'");

    Console.WriteLine();
    Console.WriteLine("After Change");
    Console.WriteLine("-------------");

    // Enable software distribution to clients.
    Console.WriteLine("Software Distribution Client Agent");
    Console.WriteLine("Current value: " + siteDefinition2["Flags"].StringValue + " (0 = Disabled, 1 = Enabled)");

    foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition2.EmbeddedProperties)
    {
        Dictionary<string, IResultObject> embeddedProperties = siteDefinition2.EmbeddedProperties; // temp copy

        // Client settings: Allow user targeted advertisement requests.
        if (kvp.Value.PropertyList["PropertyName"] == "Request User Policy")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Request User Policy"]["Value"].StringValue);
        }

        // Client settings: Policy polling interval (minutes).
        if (kvp.Value.PropertyList["PropertyName"] == "Policy Refresh Interval")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Policy Refresh Interval"]["Value"].StringValue);
        }

        // When new advertised programs are available: Display a notification message.
        if (kvp.Value.PropertyList["PropertyName"] == "Visible Signal on Available")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Visible Signal on Available"]["Value"].StringValue);
        }

        // When new advertised programs are available: Play a sound.
        if (kvp.Value.PropertyList["PropertyName"] == "Audible Signal on Available")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Audible Signal on Available"]["Value"].StringValue);
        }

        // When a scheduled program is about to run: Provide a countdown.
        if (kvp.Value.PropertyList["PropertyName"] == "Countdown Signal")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Countdown Signal"]["Value"].StringValue);
        }

        // Countdown length (minutes).
        if (kvp.Value.PropertyList["PropertyName"] == "Countdown Minutes")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Countdown Minutes"]["Value"].StringValue);
        }

        // Show advertised program notification icons in the notification area.
        if (kvp.Value.PropertyList["PropertyName"] == "Show Icon")
        {
            Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);
            Console.WriteLine("Current value: " + embeddedProperties["Show Icon"]["Value"].StringValue);
        }
    }

    Console.WriteLine(" ");
}

    catch (SmsException ex)
    {
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);
        throw;
    }

}
```

 The example method has the following parameters:

|Parameter|Type|Description|
|---------------|----------|-----------------|
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|
|`siteCode`<br /><br /> `siteToChange`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|
|`enableDisableSWDClientAgent`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable the client agent.|
|`setPolicyRefreshInterval`|-   Managed: `String`<br />-   VBScript: `String`|Policy polling interval, in minutes.|
|`enableDisableRequestUserPolicy`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable targeted advertisement requests.|
|`enableDisableVisibleSignalOnAvailable`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable display of a notification when new advertised programs are available.|
|`enableDisableAudibleSignalonAvailable`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable an audible notification when new advertised programs are available.|
|`enableDisableCountdownSignal`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable a countdown when a scheduled program is about to run.|
|`setCountdownMinutes`|-   Managed: `String`<br />-   VBScript: `String`|Countdown length, in minutes.|
|`enableDisableShowIcon`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable the display of advertised program notification icons in the notification area.|

## Compiling the Code
 The C# example requires:

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
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).

## .NET Framework Security
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).

## See Also
 [Software distribution overview](software-distribution-overview.md)
 [About software distribution setup and configuration](about-software-distribution-setup-and-configuration.md)
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
