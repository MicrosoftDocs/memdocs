---
title: How to Configure Automatic Software Metering Rule Generation
titleSuffix: Configuration Manager
description: You configure Automatic Software Metering Rule Generation settings, in Configuration Manager, by modifying the site control file.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: 7b4ff9a8-096d-4830-a4fa-c76237419e8d
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# How to Configure Automatic Software Metering Rule Generation
You configure Automatic Software Metering Rule Generation settings, in Configuration Manager, by modifying the site control file.  

> [!IMPORTANT]
>  This setting is shared across the whole hierarchy, and only can be configured on the CAS or a standalone primary site.  

### To configure automatic software metering rule generation  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Software Metering Client Agent section of the site control file by using the [SMS_SCI_ClientComp](../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the property changes to the site control file.  

## Example  
 The following example method configures various Software Metering Rule Generation settings by using the [SMS_SCI_ClientComp](../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class to connect to the site control file and change properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureAutomaticSWMRuleGeneration(swbemServices,                  _  
                                        swbemContext,                   _  
                                        siteCode,                       _       
                                        enableAutoCreateDisabledRule,   _  
                                        newAutoCreatePercentage,        _  
                                        newAutoCreateThreshold)  

    ' Load site control file and get the SMS_SCI_ClientComp section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_ClientComp " &   _  
    "WHERE ClientComponentName  = 'Software Metering Agent'" & _  
    "AND SiteCode = '" & siteCode & "'"   

     Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)     

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        'Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Auto Create Disabled Rule  
            If vProperty.PropertyName = "Auto Create Disabled Rule" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                'Modify the value.  
                vProperty.Value = enableAutoCreateDisabledRule  
                wscript.echo "New value " & enableAutoCreateDisabledRule  
            End If             

            ' Setting: Auto Create Percentage  
            If vProperty.PropertyName = "Auto Create Percentage" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newAutoCreatePercentage  
                wscript.echo "New value " & newAutoCreatePercentage  
            End If             

            ' Setting: Auto Create Threshold  
            If vProperty.PropertyName = "Auto Create Threshold" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newAutoCreateThreshold  
                wscript.echo "New value " & newAutoCreateThreshold  
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

public void ConfigureAutomaticSWMRuleGeneration(WqlConnectionManager connection,  
                                                string siteCode,  
                                                string enableAutoCreateDisabledRule,  
                                                string newAutoCreatePercentage,  
                                                string newAutoCreateThreshold)  
{  
    try  
    {  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Software Metering Agent'");  

        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Create temporary working copy of embedded properties.  
            Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

            //Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  

            // Setting: Auto Create Disabled Rule  
            if (kvp.Value.PropertyList["PropertyName"] == "Auto Create Disabled Rule")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["Auto Create Disabled Rule"]["Value"].StringValue);  

                // Change value using the enableAutoCreateDisabledRule value passed in.   
                embeddedProperties["Auto Create Disabled Rule"]["Value"].StringValue = enableAutoCreateDisabledRule;  
                Console.WriteLine("New value    : " + enableAutoCreateDisabledRule);  
            }  

            // Setting: Auto Create Percentage  
            if (kvp.Value.PropertyList["PropertyName"] == "Auto Create Percentage")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["Auto Create Percentage"]["Value"].StringValue);  

                // Change value using the newAutoCreatePercentage value passed in.   
                embeddedProperties["Auto Create Percentage"]["Value"].StringValue = newAutoCreatePercentage;  
                Console.WriteLine("New value    : " + newAutoCreatePercentage);  
            }  

            // Setting: Auto Create Threshold  
            if (kvp.Value.PropertyList["PropertyName"] == "Auto Create Threshold")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + embeddedProperties["Auto Create Threshold"]["Value"].StringValue);  

                // Change value using the newAutoCreateThreshold value passed in.   
                embeddedProperties["Auto Create Threshold"]["Value"].StringValue = newAutoCreateThreshold;  
                Console.WriteLine("New value    : " + newAutoCreateThreshold);  
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

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`enableAutoCreateDisabledRule`|-   Managed: `String`<br />-   VBScript: `String`|Enables or disables Software Metering auto rule creation.<br /><br /> -   0 - Disabled<br />-   1 - Enabled|  
|`newAutoCreatePercentage`|-   Managed: `String`<br />-   VBScript: `String`|Sets the auto creation percentage.<br /><br /> 0 - 100|  
|`newAutoCreateThreshold`|-   Managed: `String`<br />-   VBScript: `String`|Sets the auto creation threshold.|  

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
 [Configuration Manager Software Development Kit](../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [About the Configuration Manager Site Control File](../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
