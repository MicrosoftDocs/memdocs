---
title: "Configure Heartbeat Discovery"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 276572f8-15b9-4c7f-9b6f-a08582de668a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Configure Heartbeat Discovery
In System Center Configuration Manager, you configure the Heartbeat Discovery settings by modifying the necessary site control file settings.  

### To configure Heartbeat Discovery  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Heartbeat Discovery section of the site control file by using the `SMS_SCI_Component` class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the changes to the site control file.  

## Example  
 The following example sets the Heartbeat Discovery settings by using the `SMS_SCI_Component` class to connect to the site control file and change properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureHeartbeatDiscoverySettings1(swbemServices,                       _  
                                         swbemContext,                        _  
                                         siteCode,                            _  
                                         serverName,                          _  
                                         newHeartbeatSiteControlFileSchedule)  

    ' Load site control file and get the SMS_SITE_CONTROL_MANAGER section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext                     

    Query = "SELECT * FROM SMS_SCI_Component " &                         _  
    "WHERE ItemName = 'SMS_SITE_CONTROL_MANAGER|" & serverName & "' " &  _     
    "AND SiteCode = '" & siteCode & "'"  

    ' Get the SMS Software Update Point properties.  
    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Display the server name.  
        wscript.echo "Server: " & SCIComponent.Name        

        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Heartbeat Site Control File Schedule.  
            If vProperty.PropertyName = "Heartbeat Site Control File Schedule" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName                 
                wscript.echo "Current value " &  vProperty.Value1     

                'Modify the value.  
                vProperty.Value1 = newHeartbeatSiteControlFileSchedule  
                wscript.echo "New value " & newHeartbeatSiteControlFileSchedule  
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

' SEPARATE EXAMPLE TO ENABLE HEARTBEAT DISCOVERY ON THE CLIENT  
Sub ConfigureHeartbeatDiscoverySettings2(swbemServices,                       _  
                                         swbemContext,                        _  
                                         siteCode,                            _  
                                         enableDisableHeartbeatDDR)  

    ' Load site control file and get the SMS_SCI_ClientConfig section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_ClientConfig " &   _  
    "WHERE ItemName  = 'Client Properties'" & _  
    "AND SiteCode = '" & siteCode & "'"   

     Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)     

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        'Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Enable Heartbeat DDR  
            If vProperty.PropertyName = "Enable Heartbeat DDR" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                'Modify the value.  
                vProperty.Value = enableDisableHeartbeatDDR  
                wscript.echo "New value " & enableDisableHeartbeatDDR  
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

public void ConfigureHeartbeatDiscoverySettings(WqlConnectionManager connection,  
                                                string siteCode,  
                                                string serverName,  
                                                string newHeartbeatSiteControlFileSchedule,  
                                                string newEnableDisableHeartbeatDDR)  
{  

    try  
    {  
    // Change the Heartbeat Site Control File Schedule value.  

        // Connect to SMS_SITE_CONTROL_MANAGER section of the site control file.  
         IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_Component.FileType=2,ItemType='Component',SiteCode='" + siteCode + "',ItemName='SMS_SITE_CONTROL_MANAGER|" + serverName + "'");  

        // Temporary copy of the embedded properties.  
        Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {                                         
            // Property: Heartbeat Site Control File Schedule  
            if (kvp.Value.PropertyList["PropertyName"] == "Heartbeat Site Control File Schedule")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["Heartbeat Site Control File Schedule"]["Value1"].StringValue);  

                embeddedProperties["Heartbeat Site Control File Schedule"]["Value1"].StringValue = newHeartbeatSiteControlFileSchedule;  
                Console.WriteLine("New value    : " + newHeartbeatSiteControlFileSchedule);  
            }  
        }  

        // Store the settings that have changed.  
        siteDefinition.EmbeddedProperties = embeddedProperties;  

        // Save the settings.   
        siteDefinition.Put();  

    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine();  
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);  
    }  

    try  
    {  
    // Change the Enable Heartbeat DDR value.  

        // Connect to SMS_SCI_ClientConfig section of the site control file.  
    IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientConfig.FileType=2,ItemType='Client Configuration',SiteCode='" + siteCode + "',ItemName='Client Properties'");  

        // Create temporary working copy of embedded properties.  
        Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Setting: Enable Heartbeat DDR  
            if (kvp.Value.PropertyList["PropertyName"] == "Enable Heartbeat DDR")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["Value"]);  

                // Change value using the newEnableDisableHeartbeatDDR value passed in.   
                embeddedProperties["Enable Heartbeat DDR"]["Value"].StringValue = newEnableDisableHeartbeatDDR;  
                Console.WriteLine("New value    : " + newEnableDisableHeartbeatDDR);  
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

||||  
|-|-|-|  
|Parameter|Type|Description|  
|-   `connection`<br />-   `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`serverName`|-   Managed: `String`<br />-   VBScript: `String`|The server name.|  
|`newHeartbeatSiteControlFileSchedule`|-   Managed: `String`<br />-   VBScript: `String`|The schedule defining how often the client will produce heartbeat data discovery records (DDRs).|  
|-   `newEnableDisableHeartbeatDDR`<br />-   `enableDisableHeartbeatDDR`|-   Managed: `String`<br />-   VBScript: `String`|A value to enable or disable the heartbeat DDR.<br /><br /> Disabled - 0<br /><br /> Enabled - 1|  

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
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Discovery](../../../../develop/core/servers/configure/discovery.md)   
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [Configuration Manager Schedules](../../../../develop/core/understand/schedules.md)   
 [How to Create a Schedule Token](../../../../develop/core/understand/how-to-create-a-schedule-token.md)
