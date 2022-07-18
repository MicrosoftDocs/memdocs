---
title: "Configure the Software Update Point"
titleSuffix: "Configuration Manager"
description: "You configure the software update point, in Configuration Manager, by modifying the site control file settings."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 021e834d-aa7c-4b82-831d-97f110f7da73
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Configure the Software Update Point
You configure the software update point, in Configuration Manager, by modifying the site control file settings.  

### To configure a software update point  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the software update point resources section of the site control file by using the [SMS_SCI_SysResUse](../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md) class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the property changes to the site control file.  

## Example  
 The following example method configures various software update point settings by using the `SMS_SCI_SysResUse` class to connect to the site control file and change the software update point properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureSoftwareUpdatePoint(swbemServices,          _  
                                 swbemContext,           _  
                                 siteCode,               _  
                                 newUseProxy,            _   
                                 newProxyName,           _  
                                 newProxyServerPort,     _  
                                 newAnonymousProxyAccess)  

    ' Load site control file and get software update point section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_SysResUse " & _  
            "WHERE RoleName = 'SMS Software Update Point' " & _  
            "AND SiteCode = '" & siteCode & "'"  

    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

         ' Display the SUP server name.  
         wscript.echo "SUP Server: " & SCIComponent.NetworkOSPath                                      

        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: UseProxy.  
            If vProperty.PropertyName = "UseProxy" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newUseProxy  
                wscript.echo "New value " & newUseProxy  
            End If  

            ' Setting: ProxyName.  
            If vProperty.PropertyName = "ProxyName" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value2                 

                ' Modify the value.  
                vProperty.Value2 = newProxyName  
                wscript.echo "New value " & newProxyName  
            End If  

            ' Setting: ProxyServerPort.  
            If vProperty.PropertyName = "ProxyServerPort" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newProxyServerPort  
                wscript.echo "New value " & newProxyServerPort  
            End If  

            ' Setting: AnonymousProxyAccess.  
            If vProperty.PropertyName = "AnonymousProxyAccess" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newAnonymousProxyAccess  
                wscript.echo "New value " & newAnonymousProxyAccess  
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

public void ConfigureSoftwareUpdatePoint(WqlConnectionManager connection,   
                                    string siteCode,   
                                    string SUPServerName,   
                                    string newUseProxy,  
                                    string newProxyName,  
                                    string newProxyServerPort,  
                                    string newAnonymousProxyAccess)  
{  
    try  
    {  

        IResultObject siteDefinition = connection.GetInstance("SMS_SCI_SysResUse.FileType=2,ItemName='[\"Display=\\\\" + SUPServerName + "\\\"]MSWNET:[\"SMS_SITE=" + siteCode + "\"]\\\\" + SUPServerName + "\\,SMS Software Update Point',ItemType='System Resource Usage',SiteCode='" + siteCode + "'");  

        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Temporary copy of the embedded properties.  
            Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

            // Setting: UseProxy.  
            if (kvp.Value.PropertyList["PropertyName"] == "UseProxy")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["UseProxy"]["Value"].StringValue);  

                // Change the value by using the newUseProxy value that is passed in.  
                embeddedProperties["UseProxy"]["Value"].StringValue = newUseProxy;  
                Console.WriteLine("New value    : " + newUseProxy);  
            }  

            // Setting: ProxyName.  
            if (kvp.Value.PropertyList["PropertyName"] == "ProxyName")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["ProxyName"]["Value2"].StringValue);  

                // Change the value by using the newProxyName value that is passed in.  
                embeddedProperties["ProxyName"]["Value2"].StringValue = newProxyName;  
                Console.WriteLine("New value    : " + newProxyName);  
            }  

            // Setting: ProxyServerPort.  
            if (kvp.Value.PropertyList["PropertyName"] == "ProxyServerPort")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["ProxyServerPort"]["Value"].StringValue);  

                // Change the value by using the newProxyServerPort value that is passed in.  
                embeddedProperties["ProxyServerPort"]["Value"].StringValue = newProxyServerPort;  
                Console.WriteLine("New value    : " + newProxyServerPort);  
            }  

            // Setting: AnonymousProxyAccess.  
            if (kvp.Value.PropertyList["PropertyName"] == "AnonymousProxyAccess")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["AnonymousProxyAccess"]["Value"].StringValue);  

                // Change the value by using the newAnonymousProxyAccess value that is passed in.  
                embeddedProperties["AnonymousProxyAccess"]["Value"].StringValue = newAnonymousProxyAccess;  
                Console.WriteLine("New value    : " + newAnonymousProxyAccess);  
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

|Parameter|Type|Description|
|---------|----|-----------|
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`SUPServerName`|-   Managed: `String`|The name of the software update point server.|  
|`newUseProxy`|-   Managed: `String`<br />-   VBScript: `String`|Determines whether to use a proxy server.<br /><br /> Possible values:<br /><br /> "0" = `false`<br /><br /> "1" = `true`|  
|`newProxyName`|-   Managed: `String`<br />-   VBScript: `String`|The proxy server name.|  
|`newProxyServerPort`|-   Managed: `String`<br />-   VBScript: `String`|The proxy server port.|  
|`newAnonymousProxyAccess`|-   Managed: `String`<br />-   VBScript: `String`|Determines whether to use credentials to connect to the proxy server. If this value is set to true, then the account used to connect needs to be set in the Configuration Manager 2007 Administrator Console.<br /><br /> Possible values:<br /><br /> "0" = `true`<br /><br /> "1" = `false`|  

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

## See Also  
 [About Software Updates Setup and Configuration](../../develop/sum/about-software-updates-setup-and-configuration.md)   
 [About the Configuration Manager Site Control File](../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md)
