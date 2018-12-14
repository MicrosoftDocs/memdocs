---
title: "Configure Network Discovery"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1b2a2766-1ada-4949-b548-af41454c0467
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Configure Network Discovery
You configure the Network Discovery settings, in System Center Configuration Manager, by modifying the necessary site control file settings.  

### To configure Network Discovery  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Network Discovery section of the site control file by using the `SMS_SCI_Component` class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the changes to the site control file.  

5.  Make a connection to the Network Discovery section of the site control file by using the `SMS_SCI_Configuration` class.  

6.  Loop through the array of available properties, making changes as needed.  

7.  Commit the changes to the site control file.  

## Example  
 The following example sets the Network Discovery settings by using the `SMS_SCI_Component` and `SMS_SCI_Configuration` classes to connect to the site control file and change properties.  

> [!NOTE]
>  Network Discovery is unusual, in that it requires setting both the `SMS_SCI_Component` and `SMS_SCI_Configuration` class properties to enable the component.  

 For information about calling the smple code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureNetworkDiscoverySettings(swbemServices,         _  
                                      swbemContext,          _  
                                      siteCode,              _  
                                      enableDisableDiscovery)  

    ' Load site control file and get the SMS_SCI_Component, SMS_NETWORK_DISCOVERY section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    ' Get the SMS_SCI_Component, SMS_NETWORK_DISCOVERY section of the site control file.   
    Query = "SELECT * FROM SMS_SCI_Component "       & _  
    "WHERE ComponentName = 'SMS_NETWORK_DISCOVERY' " & _  
    "AND SiteCode = '" & siteCode & "'"  

    ' Get the SMS_NETWORK_DISCOVERY properties.  
    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Display the server name.  
        wscript.echo "Server: " & SCIComponent.Name        

        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Discovery Enabled  
            If vProperty.PropertyName = "Discovery Enabled" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value: " &  vProperty.Value1                 

                ' Modify the value.  
                vProperty.Value1 = enableDisableDiscovery  
                wscript.echo "New value:     " & enableDisableDiscovery  
            End If  

         Next  

         ' Update the component in your copy of the site control file. Get the path  
         ' to the updated object, which could be used later to retrieve the instance.  
          Set SCICompPath = SCIComponent.Put_(wbemChangeFlagUpdateOnly, swbemContext)  

    Next  

    ' Get the SMS_SCI_Configuration, SMS_NETWORK_DISCOVERY section of the site control file.                      
    Query = "SELECT * FROM SMS_SCI_Configuration "       & _  
    "WHERE ItemName = 'SMS_NETWORK_DISCOVERY' " & _  
    "AND SiteCode = '" & siteCode & "'"  

    ' Get the SMS_NETWORK_DISCOVERY properties.  
    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Discovery Enabled  
            If vProperty.PropertyName = "Discovery Enabled" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value: " &  vProperty.Value1                 

                ' Modify the value.  
                vProperty.Value1 = enableDisableDiscovery  
                wscript.echo "New value:     " & enableDisableDiscovery  
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

public void ConfigureNetworkDiscoverySettings(WqlConnectionManager connection,  
                                              string siteCode,  
                                              string serverName,  
                                              string enableDisableDiscovery)  

{  
    try  
    {  
        // Connect to SMS_SCI_Component, SMS_NETWORK_DISCOVERY section of the site control file.  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_Component.FileType=2,ItemType='Component',SiteCode='" + siteCode + "',ItemName='SMS_NETWORK_DISCOVERY|" + serverName + "'");  

        // Create temporary copy of the embedded properties.  
        Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

        // Enumerate through the embedded properties and makes changes as needed.  
        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Setting: Discovery Enabled  
            if (kvp.Value.PropertyList["PropertyName"] == "Discovery Enabled")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["Value1"]);  

                // Change value using the newDiscoveryEnabled value passed in.   
                embeddedProperties["Discovery Enabled"]["Value1"].StringValue = enableDisableDiscovery;  
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
        Console.WriteLine();  
        Console.WriteLine("Failed. Error: " + ex.InnerException.Message);  
    }  

    try  
    {  
        // Connect to SMS_SCI_Configuration, SMS_NETWORK_DISCOVERY section of the site control file.  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_Configuration.FileType=2,ItemType='Configuration',SiteCode='" + siteCode + "',ItemName='SMS_NETWORK_DISCOVERY'");  

        // Create temporary copy of the embedded properties.  
        Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

        // Enumerate through the embedded properties and makes changes as needed.  
        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Setting: Discovery Enabled  
            if (kvp.Value.PropertyList["PropertyName"] == "Discovery Enabled")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["Value1"]);  

                // Change value using the newDiscoveryEnabled value passed in.   
                embeddedProperties["Discovery Enabled"]["Value1"].StringValue = enableDisableDiscovery;  
                Console.WriteLine("New value    : " + enableDisableDiscovery);  
            }  
        }  

        // Store the settings that have changed.  
        siteDefinition.EmbeddedProperties = embeddedProperties;  

        //Save the settings.   
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
|`enableDisableDiscovery`|-   Managed: `String`<br />-   VBScript: `String`|A value to enable or disable the discovery method.<br /><br /> Disabled - `false`<br /><br /> Enabled - `true`|  

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
