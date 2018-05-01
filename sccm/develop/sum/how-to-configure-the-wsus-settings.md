---
title: "Configure the WSUS Settings"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: c6d0f7c3-d794-4f15-89ce-dbdbb57d133c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Configure the WSUS Settings
You configure the Windows Server Update Services (WSUS) component settings, in System Center Configuration Manager, by modifying the site control file. For more information about WSUS, see the MSDN documentation for [Windows Server Update Services](http://go.microsoft.com/fwlink/?LinkId=93575).  

### To configure WSUS settings  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the WSUS Configuration Manager component section of the site control file by using the [SMS_SCI_Component](../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md) class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the property changes to the site control file.  

## Example  
 The following example method configures various Windows Server Update Services (WSUS) component settings by using the [SMS_SCI_Component](../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md) class to connect to the site control file and change properties.  

> [!NOTE]
>  For configuration related information and values, see the Configuring Software Updates section of the System Center Configuration Manager documentation at [http://go.microsoft.com/fwlink/?LinkId=111682](http://go.microsoft.com/fwlink/?LinkId=111682).  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureWSUSSettings(swbemServices,         _  
                          swbemContext,          _  
                          siteCode,              _  
                          newDefaultWSUSIISPort, _  
                          newSSLDefaultWSUS,     _  
                          newDefaultWSUSIISSSLPort)  

    ' Load site control file and get the SMS_WSUS_CONFIGURATION_MANAGER component section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_Component " & _  
            "WHERE ComponentName = 'SMS_WSUS_CONFIGURATION_MANAGER' " & _  
            "AND SiteCode = '" & siteCode & "'"  

    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Display the WSUS server name.  
            If vProperty.PropertyName = "DefaultWSUS" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName & " Server: " & vProperty.Value2                
            End If  

            ' Setting: DefaultWSUSIISPort.  
            If vProperty.PropertyName = "DefaultWSUSIISPort" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newDefaultWSUSIISPort  
                wscript.echo "New value " & newDefaultWSUSIISPort  
            End If  

            ' Setting: SSLDefaultWSUS.  
            If vProperty.PropertyName = "SSLDefaultWSUS" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newSSLDefaultWSUS  
                wscript.echo "New value " & newSSLDefaultWSUS  
            End If  

            ' Setting: DefaultWSUSIISSSLPort.  
            If vProperty.PropertyName = "DefaultWSUSIISSSLPort" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newDefaultWSUSIISSSLPort  
                wscript.echo "New value " & newDefaultWSUSIISSSLPort  
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

public void ConfigureWSUSSettings(WqlConnectionManager connection,   
                                    string siteCode,   
                                    string SUPServerName,   
                                    string newDefaultWSUSIISPort,  
                                    string newSSLDefaultWSUS,  
                                    string newDefaultWSUSIISSSLPort)  
{  
    try  
    {  
        // Connect to SMS_WSUS_CONFIGURATION_MANAGER section of the site control file.  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_Component.FileType=2,ItemType='Component',SiteCode='" + siteCode + "',ItemName='SMS_WSUS_CONFIGURATION_MANAGER|" + SUPServerName + "'");  
        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Temporary copy of the embedded properties.  
            Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

            // Display the WSUS server name.  
            if (kvp.Value.PropertyList["PropertyName"] == "DefaultWSUS")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"] + " Server");  
                Console.WriteLine("Server name: " + embeddedProperties["DefaultWSUS"]["Value2"].StringValue);                      
            }  

            // Setting: DefaultWSUSIISPort.  
            if (kvp.Value.PropertyList["PropertyName"] == "DefaultWSUSIISPort")  
            {  
                Console.WriteLine();   
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["DefaultWSUSIISPort"]["Value"].StringValue);  

                // Change the value by using the newDefaultWSUSIISPort value passed that is in.  
                embeddedProperties["DefaultWSUSIISPort"]["Value"].StringValue = newDefaultWSUSIISPort;  
                Console.WriteLine("New value    : " + newDefaultWSUSIISPort);  
            }  

            // Setting: SSLDefaultWSUS.  
            if (kvp.Value.PropertyList["PropertyName"] == "SSLDefaultWSUS")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["SSLDefaultWSUS"]["Value"].StringValue);  

                // Change the value by using the newSSLDefaultWSUS value that is passed in.  
                embeddedProperties["SSLDefaultWSUS"]["Value"].StringValue = newSSLDefaultWSUS;  
                Console.WriteLine("New value    : " + newSSLDefaultWSUS);  
            }  

            // Setting: DefaultWSUSIISSSLPort.  
            if (kvp.Value.PropertyList["PropertyName"] == "DefaultWSUSIISSSLPort")  
            {  
                Console.WriteLine();   
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["DefaultWSUSIISSSLPort"]["Value"].StringValue);  

                // Change the value by using the newDefaultWSUSIISSSLPort value that is passed in.  
                embeddedProperties["DefaultWSUSIISSSLPort"]["Value"].StringValue = newDefaultWSUSIISSSLPort;  
                Console.WriteLine("New value    : " + newDefaultWSUSIISSSLPort);  
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
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`SUPServerName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the software update point server.|  
|`newDefaultWSUSIISPort`|-   Managed: `String`<br />-   VBScript: `String`|The new default WSUS Internet Information Services (IIS) port.|  
|`newSSLDefaultWSUS`|-   Managed: `String`<br />-   VBScript: `String`|Determines whether to use Secure Sockets Layer (SSL).|  
|`newDefaultWSUSIISSSLPort`|-   Managed: `String`<br />-   VBScript: `String`|Identifies the default WSUS IIS SSL port.|  

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
 [Software Updates Setup and Configuration](../../develop/sum/software-updates-setup-and-configuration.md)   
 [About Software Updates Setup and Configuration](../../develop/sum/about-software-updates-setup-and-configuration.md)   
 [About the Configuration Manager Site Control File](../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md)
