---
title: Set Operating System Deployment Branding Information
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 95a1f0b7-2568-403f-bd24-43abc859eaf0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
description: Learn how to set operating system deployment branding information in the configuration manager by changing the property of the client agent component section.
ms.reviewer: mstewart,aaroncz 
---
# How to Set Operating System Deployment Branding Information in Configuration Manager
You set the operating system deployment branding information for the Configuration Manager client by changing the `OSDBrandingSubtitle` property of the client agent component section in the site control file.  

> [!NOTE]
>  `OSDBrandingSubtitle` is encoded with BASE64 encoding.  

 The branding information is displayed by the task sequence when it is run on the client.  

### To set operating system deployment branding information  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](../core/understand/sms-provider-fundamentals.md) .  

2.  Get the client agent site control file client component object from [SMS_SCI_ClientComp Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md).  

3.  Set the `OSDBrandingSubtitle` property to the value you want.  

4.  Commit the changes back to the site control file.  

## Example  
 The following example method changes the operating system deployment branding text to the supplied value.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub SetOsdBranding(connection,          _  
                      context,          _  
                      siteCode,               _  
                      brandingText)  

    ' Load the site control file and get the Client Agent section.  
    connection.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , context  

    Query = "SELECT * FROM SMS_SCI_ClientComp " & _  
            "WHERE ClientComponentName = 'Client Agent' " & _  
            "AND SiteCode = '" & siteCode & "'"  

    Set SCIComponentSet = connection.ExecQuery(Query, ,wbemFlagForwardOnly Or wbemFlagReturnImmediately, context)  

    ' Only one instance is returned from the query.  
    For Each SCIComponent In SCIComponentSet                                

        ' Loop through the array of embedded SMS_EmbeddedProperty instances.  
        For Each vProperty In SCIComponent.Props  

            ' Setting: OSDBrandingSubTitle.  
            If vProperty.PropertyName = "OSDBrandingSubTitle" Then  
                wscript.echo " "  
                wscript.echo vProperty.PropertyName  
                wscript.echo "Current value " &  vProperty.Value1                 

                ' Modify the value.  
                vProperty.Value1 = brandingText  
                wscript.echo "New value: " & brandingText  
            End If  

        Next     

             ' Update the component in your copy of the site control file. Get the path  
             ' to the updated object, which can be used later to retrieve the instance.  
              Set SCICompPath = SCIComponent.Put_(wbemChangeFlagUpdateOnly, context)  
    Next  

    ' Commit the change to the actual site control file.  
    Set InParams = connection.Get("SMS_SiteControlFile").Methods_("CommitSCF").InParameters.SpawnInstance_  
    InParams.SiteCode = siteCode  
    connection.ExecMethod "SMS_SiteControlFile", "CommitSCF", InParams, , context  

End Sub  
```  

```c#  
public void SetOsdBranding(  
    WqlConnectionManager connection,   
    string siteCode,   
    string brandingText)  
{  
    try  
    {  
        // Get the site control file client component section.  
        IResultObject clientAgent = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" +   
            siteCode + "',ItemName='Client Agent'");  

        // Update the branding information.  
        Dictionary<string, IResultObject> embeddedProperties = clientAgent.EmbeddedProperties;  

        embeddedProperties["OSDBrandingSubTitle"]["Value1"].StringValue = brandingText;  

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
|`connection`|-   Managed: `WqlConnectionManager`<br />-   VBScript: `SWbemServices`|A valid connection to the SMS Provider.|  
|`context (VBScript)`|-   VBScript: `SWbemContext`|A valid context qualifier object. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using WMI](../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md)|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code for the Configuration Manager site.|  
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
 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

## See Also  
 [SMS_SCI_ClientComp Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md)   
 [About OS deployment site role configuration](about-operating-system-deployment-site-role-configuration.md)
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)
