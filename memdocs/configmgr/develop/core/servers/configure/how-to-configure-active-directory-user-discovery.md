---
description: Learn how to configure the Active Directory User Discovery settings by modifying the necessary site control file settings.
title: Configure Active Directory User Discovery
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: d64464a2-dba8-4e87-a487-bfdeb9073e12
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Configure Active Directory User Discovery
In Configuration Manager, you configure the Active Directory User Discovery settings by modifying the necessary site control file settings.  

### To configure Active Directory User Discovery  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Active Directory User Discovery section of the site control file by using the `SMS_SCI_Component` class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the changes to the site control file.  

## Example  
 The following example sets the Active Directory User Discovery settings by using the `SMS_SCI_Component` class to connect to the site control file and change properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureADUserDiscoverySettings(swbemServices,           _  
                                     swbemContext,            _  
                                     siteCode,                _  
                                     serverName,              _  
                                     newStartupSchedule,      _  
                                     enableDisableDiscovery)  

    ' Load site control file and get the SMS_AD_USER_DISCOVERY_AGENT section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_Component " &                         _  
    "WHERE ItemName = 'SMS_AD_USER_DISCOVERY_AGENT|" & serverName & "' " &  _     
    "AND SiteCode = '" & siteCode & "'"  

    ' Get the SMS_AD_USER_DISCOVERY_AGENT properties.  
    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Display the server name.  
        wscript.echo "Server: " & SCIComponent.Name        

        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Startup Schedule  
            If vProperty.PropertyName = "Startup Schedule" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value1                 

                ' Modify the value.  
                vProperty.Value1 = newStartupSchedule  
                wscript.echo "New value " & newStartupSchedule  
            End If  

            ' Setting: SETTINGS  
            If vProperty.PropertyName = "SETTINGS" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value1                 

                ' Modify the value.  
                vProperty.Value1 = enableDisableDiscovery  
                wscript.echo "New value " & enableDisableDiscovery  
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

public void ConfigureADUserDiscoverySettings(WqlConnectionManager connection,  
                                             string siteCode,  
                                             string serverName,  
                                             string newStartupSchedule,  
                                             string enableDisableDiscovery)  
{  
    try  
    {  
        // Connect to SMS_AD_USER_DISCOVERY_AGENT section of the site control file.  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_Component.FileType=2,ItemType='Component',SiteCode='" + siteCode + "',ItemName='SMS_AD_USER_DISCOVERY_AGENT|" + serverName + "'");  

        // Create temporary copy of the embedded properties.  
        Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

        // Enumerate through the embedded properties and makes changes as needed.  
        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Setting: Startup Schedule  
            if (kvp.Value.PropertyList["PropertyName"] == "Startup Schedule")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["Value1"]);  

                // Change value using the newStartupSchedule value passed in.   
                embeddedProperties["Startup Schedule"]["Value1"].StringValue = newStartupSchedule;  
                Console.WriteLine("New value    : " + newStartupSchedule);  
            }  

            // Setting: SETTINGS                      
            if (kvp.Value.PropertyList["PropertyName"] == "SETTINGS")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["Value1"]);  

                // Change value using the enableDisableDiscovery value passed in.   
                embeddedProperties["SETTINGS"]["Value1"].StringValue = enableDisableDiscovery;  
                Console.WriteLine("New value    : " + enableDisableDiscovery);  
            }  
        }  

        // Store the settings that have changed.  
        siteDefinition.EmbeddedProperties = embeddedProperties;  

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

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|-   `connection`<br />-   `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`serverName`|-   Managed: `String`<br />-   VBScript: `String`|The server name.|  
|`newStartupSchedule`|-   Managed: `String`<br />-   VBScript: `String`|The new schedule.|  
|`enableDisableDiscovery`|-   Managed: `String`<br />-   VBScript: `String`|A value to enable or disable the discovery method.<br /><br /> Disabled - INACTIVE<br /><br /> Enabled - ACTIVE|  

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
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Configuration Manager role-based administration](../../../../develop/core/servers/configure/role-based-administration.md).  

## See Also  
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [About schedules](../../understand/about-configuration-manager-schedules.md)
 [How to Create a Schedule Token](../../../../develop/core/understand/how-to-create-a-schedule-token.md)
