---
title: "Configure Software Inventory Settings"
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
ms.assetid: ddbee23e-5495-4864-a0e0-49555ad18f12searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Configure Software Inventory Settings
You set the Software Inventory Client Agent settings, in System Center Configuration Manager, by modifying the necessary site control file settings.  

### To modify the Software Inventory Client Agent settings  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Software Inventory Client Agent section of the site control file by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the changes to the site control file.  

## Example  
 The following example sets the Software Inventory Client Agent settings by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class to connect to the site control file and change properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ConfigureSoftwareInventoryClientAgentSettings(swbemServices,             _  
                                                  swbemContext,              _  
                                                  siteCode,                  _  
                                                  enableDisableClientAgent,  _  
                                                  newInventorySchedule)  

    ' Load site control file and get the SMS_SCI_ClientComp section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  

    Query = "SELECT * FROM SMS_SCI_ClientComp " & _  
    "WHERE ClientComponentName = 'Software Inventory Agent' " & _  
    "AND SiteCode = '" & siteCode & "'"            

    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  

    'Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet  

        ' Set the client agent by setting the Flags value to 0 or 1 using the enableDisableClientAgent variable.  
        wscript.echo " "  
        wscript.echo "Software Inventory Agent"  
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

        Next     

        'Update the component in your copy of the site control file. Get the path  
        'to the updated object, which could be used later to retrieve the instance.  
         Set SCICompPath = SCIComponent.Put_(wbemChangeFlagUpdateOnly, swbemContext)  

    Next  

    'Commit the change to the actual site control file.  
    Set InParams = swbemServices.Get("SMS_SiteControlFile").Methods_("CommitSCF").InParameters.SpawnInstance_  
    InParams.SiteCode = siteCode  
    swbemServices.ExecMethod "SMS_SiteControlFile", "CommitSCF", InParams, , swbemContext  

End Sub  

```  

```c#  

public void ConfigureSoftwareInventoryClientAgentSettings(WqlConnectionManager connection,  
                                                          string siteCode,  
                                                          string enableDisableClientAgent,  
                                                          string newInventorySchedule)  
{  
    try  
    {  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Software Inventory Agent'");  

        // Setting: Enable Client Agent  
        // Enable or disable the client agent by setting the Flags value to 0 or 1 using the enableDisableClientAgent variable.   
        Console.WriteLine();  
        Console.WriteLine("Software Update Client Agent");  
        Console.WriteLine("Current value: " + siteDefinition["Flags"].StringValue);  

        // Change value using the enableDisableSUMClientAgent value passed in.   
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
                Console.WriteLine("Current value: " + embeddedProperties[kvp.Value.PropertyList["PropertyName"]]["Value2"].StringValue);  

                // Change value using the newEvaluationSchedule value passed in.   
                embeddedProperties["Inventory Schedule"]["Value2"].StringValue = newInventorySchedule;  
                Console.WriteLine("New value    : " + newInventorySchedule);  
            }  

            // Store the settings that have changed.  
            siteDefinition.EmbeddedProperties = embeddedProperties;  
        }  

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
|`enableDisableClientAgent`|-   Managed: `String`<br />-   VBScript: `String`|A value to enable or disable the client agent.<br /><br /> Disabled - 0<br /><br /> Enabled - 1|  
|`newInventorySchedule`|-   Managed: `String`<br />-   VBScript: `String`|A value to set the inventory schedule.|  
|`newScanInterval`|-   Managed: `String`<br />-   VBScript: `String`|A value to set the scan interval.|  

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
 [Configuration Manager Inventory](../../../../develop/core/clients/inventory/inventory.md)   
 [About Configuration Manager Inventory](../../../../develop/core/clients/inventory/about-configuration-manager-inventory.md)   
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [Configuration Manager Schedules](../../../../develop/core/understand/schedules.md)   
 [How to Create a Schedule Token](../../../../develop/core/understand/how-to-create-a-schedule-token.md)
