---
title: "Configure Hardware Inventory Settings"
titleSuffix: "Configuration Manager"
description: "Set the Hardware Inventory Client Agent settings by modifying the necessary site control file settings."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 3ecabdc0-04e5-42ff-9578-97f9874698ad
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3


---
# How to Configure Hardware Inventory Settings
You set the Hardware Inventory Client Agent settings, in Configuration Manager, by modifying the necessary site control file settings.  

### To modify the Hardware Inventory Client Agent settings  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Hardware Inventory Client Agent section of the site control file by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the changes to the site control file.  

## Example  
 The following example sets the Hardware Inventory Client Agent settings by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class to connect to the site control file and change properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureHardwareInventoryClientAgentSettings(swbemServices,        _  
                                                  swbemContext,         _  
                                                  siteCode,             _  
                                                  newInventorySchedule, _  
                                                  newMIFSize,           _   
                                                  newMIFCollection)  

    ' Load site control file and get the SMS Software Update Point system resource section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_ClientComp " & _  
    "WHERE ClientComponentName = 'Hardware Inventory Agent' " & _  
    "AND SiteCode = '" & siteCode & "'"            

    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Set the client agent by setting the Flags value to 0 or 1 using the enableDisableClientAgent variable.  
        wscript.echo " "  
        wscript.echo "Hardware Inventory Agent"  
        wscript.echo "Current value " &  SCIComponent.Flags  

        ' Modify the value.                  
        SCIComponent.Flags = enableDisableClientAgent  
        wscript.echo "New value " & enableDisableClientAgent  

        'Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: Inventory Schedule  
            If vProperty.PropertyName = "Inventory Schedule" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value2                 

                'Modify the value.  
                vProperty.Value2 = newInventorySchedule  
                wscript.echo "New value " & newInventorySchedule  
            End If  

            ' Setting: Maximum 3rd Party MIF Size  
            If vProperty.PropertyName = "Maximum 3rd Party MIF Size" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newMIFSize  
                wscript.echo "New value " & newMIFSize  
            End If  

            ' Setting: MIF Collection  
            If vProperty.PropertyName = "MIF Collection" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value                 

                ' Modify the value.  
                vProperty.Value = newMIFCollection  
                wscript.echo "New value " & newMIFCollection  
            End If  

        Next     

        ' Update the component in your copy of the site control file. Get the path  
        'to the updated object, which could be used later to retrieve the instance.  
        Set SCICompPath = SCIComponent.Put_(wbemChangeFlagUpdateOnly, swbemContext)  

    Next  

    ' Commit the change to the actual site control file.  
    Set InParams = swbemServices.Get("SMS_SiteControlFile").Methods_("CommitSCF").InParameters.SpawnInstance_  
    InParams.SiteCode = siteCode  
    swbemServices.ExecMethod "SMS_SiteControlFile", "CommitSCF", InParams, , swbemContext  

End Sub  
```  

```c#  

public void ConfigureHardwareInventoryClientAgentSettings(WqlConnectionManager connection,  
                                                    string siteCode,  
                                                    string enableDisableClientAgent,  
                                                    string newInventorySchedule,  
                                                    string newMIFSize,  
                                                    string newMIFCollection)  
{  
    try  
    {  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Hardware Inventory Agent'");  

        // Setting: Enable Client Agent  
        // Enable or disable the client agent by setting the Flags value to 0 or 1 using the enableDisableClientAgent variable.   
        Console.WriteLine();  
        Console.WriteLine("Hardware Inventory Client Agent");  
        Console.WriteLine("Current value: " + siteDefinition["Flags"].StringValue);  

        // Change value using the enableDisableClientAgent value passed in.   
        siteDefinition["Flags"].StringValue = enableDisableClientAgent;  
        Console.WriteLine("New value    : " + enableDisableClientAgent);  

        foreach (KeyValuePair<string, IResultObject> kvp in siteDefinition.EmbeddedProperties)  
        {  
            // Create temporary working copy of embedded properties.  
            Dictionary<string, IResultObject> embeddedProperties = siteDefinition.EmbeddedProperties;  

            // Setting: Inventory Schedule  
            if (kvp.Value.PropertyList["PropertyName"] == "Inventory Schedule")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["PropertyName"]);  

                // Change value using the newInventorySchedule value passed in.   
                embeddedProperties["Inventory Schedule"]["Value2"].StringValue = newInventorySchedule;  
                Console.WriteLine("New value    : " + newInventorySchedule);  
            }  

            // Setting: Maximum 3rd Party MIF Size  
            if (kvp.Value.PropertyList["PropertyName"] == "Maximum 3rd Party MIF Size")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["PropertyName"]);  

                // Change value using the newMIFSize value passed in.   
                embeddedProperties["Maximum 3rd Party MIF Size"]["Value"].StringValue = newMIFSize;  
                Console.WriteLine("New value    : " + newMIFSize);  
            }  

            // Setting: MIF Collection  
            if (kvp.Value.PropertyList["PropertyName"] == "MIF Collection")  
            {  
                Console.WriteLine();  
                Console.WriteLine(kvp.Value.PropertyList["PropertyName"]);  
                Console.WriteLine("Current value: " + kvp.Value.PropertyList["PropertyName"]);  

                // Change value using the newMIFCollection value passed in.   
                embeddedProperties["MIF Collection"]["Value"].StringValue = newMIFCollection;  
                Console.WriteLine("New value    : " + newMIFCollection);  
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
|-   `connection`<br />-   `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`enableDisableClientAgent`|-   Managed: `String`<br />-   VBScript: `String`|A value to enable or disable the client agent.<br /><br /> Disabled - 0<br /><br /> Enabled - 1|  
|`newInventorySchedule`|-   Managed: `String`<br />-   VBScript: `String`|A value to set the inventory schedule.|  
|`newMIFSize`|-   Managed: `String`<br />-   VBScript: `String`|A value to set the maximum size of the hardware inventory MIF.<br /><br /> Default is 512.|  
|`newMIFCollection`|-   Managed: `String`<br />-   VBScript: `String`|A value to enable or disable MIF collection.<br /><br /> Collect:<br /><br /> No (MIF) files - 0<br /><br /> NOIDMIF files - 4<br /><br /> IDMIF files - 8<br /><br /> Both NOIDMIF and IDMIF files - 12|  

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
 [About Configuration Manager Inventory](../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md)   
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [About schedules](../../understand/about-configuration-manager-schedules.md)
 [How to Create a Schedule Token](../../../../develop/core/understand/how-to-create-a-schedule-token.md)
