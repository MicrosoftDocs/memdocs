---
title: "How to Customize Advertisement Branding Information in Configuration Manager"
ms.custom: ""
ms.date: "2016-09-20"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "System Center Configuration Manager (current branch)"
ms.assetid: 536e192b-2a77-4542-950f-e05b04074e41
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Customize Advertisement Branding Information in Configuration Manager
You set the software distribution branding information for the System Center Configuration Manager client by changing the `SWDBrandingSubTitle` property of the client agent component section in the site control file.  
  
### To customize advertisement branding information  
  
1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  
  
2.  Get the Client Agent site control file `Client Component` object from [SMS_SCI_ClientComp Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md).  
  
3.  Set the `SWDBrandingSubtitle` property to the value you want.  
  
4.  Commit the changes back to the site control file.  
  
## Example  
 The following example method changes the software distribution branding text to the supplied value.  
  
 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling code snippets.md).  
  
```vbs  
  
Sub SetAdvertBranding(swbemServices,          _  
                      swbemContext,           _  
                      siteCode,               _  
                      brandingText)  
  
    ' Load the site control file and get the Client Agent section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  
  
    Query = "SELECT * FROM SMS_SCI_ClientComp " & _  
            "WHERE ClientComponentName = 'Client Agent' " & _  
            "AND SiteCode = '" & siteCode & "'"  
  
    Set SCIComponentSet = swbemServices.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, swbemContext)  
  
    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet                                
  
        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  
  
            ' Setting: SWDBrandingSubTitle  
            If vProperty.PropertyName = "SWDBrandingSubTitle" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value1                 
  
                ' Modify the value.  
                vProperty.Value1 = brandingText  
                wscript.echo "New value: " & brandingText  
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
public void SetAdvertBranding(WqlConnectionManager connection, string siteCode,  string brandingText)  
{  
    try  
    {  
        // Get the site control file client component section.  
        IResultObject clientAgent = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Client Agent'");  
  
        // Update the branding information.  
        Dictionary<string, IResultObject> embeddedProperties = clientAgent.EmbeddedProperties;  
  
        embeddedProperties["SWDBrandingSubTitle"]["Value1"].StringValue=brandingText;  
  
        clientAgent.EmbeddedProperties = embeddedProperties;  
        // Commit the change back to the site control file.  
        clientAgent.Put();  
  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to set branding text: " + e.Message);  
        throw;  
    }  
}  
```  
  
 The example method has the following parameters:  
  
|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swbemServices`|-   Managed: [WqlConnectionManager](assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True)<br />-   VBScript: [SWbemServices](assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code for the System Center Configuration Manager site.|  
|`brandingText`|-   Managed: `String`<br />-   VBScript: `String`|The text used to update the branding text.|  
  
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
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software distribution.md)   
 [Software Distribution Setup and Configuration](../../../../develop/core/servers/configure/software-distribution-setup-and-configuration.md)   
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/7fc4e08d-bccf-4616-a789-71070d3c6f7b.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/815a4ee8-b211-48de-ba9f-6eff7497dd2b.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)