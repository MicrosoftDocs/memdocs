---
title: "Enable or Disable the Advertised Programs Client Agent"
titleSuffix: "Configuration Manager"
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
ms.assetid: c6fcffc5-4695-4de5-9ec3-90595239049bsearchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Enable or Disable the Software Distribution Advertised Programs Client Agent
In System Center Configuration Manager, the site control file maintains configuration for the site. This topic shows how to enable or disable the Software Distribution Advertised Programs Client Agent setting in the site control file. Details about reading from and writing to the site control file are discussed in the [Configuration Manager Site Control File](../../../../develop/core/understand/site-control-file.md) section of the Configuration Manager SDK.  

> [!CAUTION]
>  You should be experienced in managing a site's configuration before using the SMS Provider classes to modify the site configuration. You should use caution or avoid using the `SMS_SCI_FileDefinition` and `SMS_SCI_SiteDefinition` classes altogether. These classes manage the site control file itself. You can cause significant damage to a site by changing some configurable items.  

### To enable or disable the client agent  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Make a connection to the software distribution client component section of the site control file by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class.  

3.  Adjust the client agent settings by setting the flag value to 0 to disable the agent or 1 to enable the agent.  

4.  Commit the property changes to the site control file.  

## Example  
 The following example method queries for the specific site control file item, software distribution client component section, and changes the flag value to enable or disable the client agent.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub EnableDisableSWDClientAgent(swbemServices, swbemContext, enableDisableFlag, siteToChange )  

    ' Load site control file and get SWD client component section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteToChange & """", "Refresh", , , swbemContext  
    Set objSWbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteToChange & "',ItemName='Software Distribution'", , swbemContext)  

    ' Display SWD client agent settings before change  
    Wscript.Echo " "  
    Wscript.Echo "Properties - Before Change"  
    Wscript.Echo "---------------------------"  
    Wscript.Echo objSWbemInst.ClientComponentName  
    Wscript.Echo objSWbemInst.Flags & " (0 = Disabled, 1 = Enabled)"  

    ' Set SWD client agent by setting Flags value to  0 or 1 using the sEnableDisableFlag variable.  
    objSWbemInst.Flags = enableDisableFlag  

    ' Save new client agent settings.  
    objSWbemInst.Put_ , swbemContext  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteToChange & """", "Commit", , , swbemContext  

    ' Refresh in-memory copy of the site control file and get the DCM client component section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteToChange & """", "Refresh", , , swbemContext  
    Set objSWbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteToChange & "',ItemName='Software Distribution'", , swbemContext)  

    ' Display SWD client agent settings after change.  
    Wscript.Echo " "  
    Wscript.Echo "Properties - After Change"  
    Wscript.Echo "---------------------------"  
    Wscript.Echo objSWbemInst.ClientComponentName  
    Wscript.Echo objSWbemInst.Flags & " (0 = Disabled, 1 = Enabled)"  

End Sub  

```  

```c#  
public void EnableDisableSWDClientAgent(WqlConnectionManager connection, string enableDisableFlag, string siteCode)  
{  
    try  
    {  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Software Distribution'");  

        // Display SWD client agent settings before change.  
        Console.WriteLine();  
        Console.WriteLine("Properties - Before Change");  
        Console.WriteLine("---------------------------");  
        Console.WriteLine(siteDefinition["ClientComponentName"].StringValue);  
        Console.WriteLine(siteDefinition["Flags"].StringValue + " (0 = Disabled, 1 = Enabled)");  

        // Set SWD client agent by setting "Flags" value to 0 or 1 using the enableDisableFlag variable.  
        siteDefinition["Flags"].StringValue = enableDisableFlag;  

        // Save the settings.  
        siteDefinition.Put();  

        // Verify change by reconnecting and getting the value again.  
        IResultObject siteDefinition2 = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Software Distribution'");  

        // Display SWD client agent settings after change.  
        Console.WriteLine();  
        Console.WriteLine("Properties - After Change");  
        Console.WriteLine("--------------------------");  
        Console.WriteLine(siteDefinition2["ClientComponentName"].StringValue);  
        Console.WriteLine(siteDefinition2["Flags"].StringValue + " (0 = Disabled, 1 = Enabled)");  
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
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`enableDisableFlag`|-   Managed: `String`<br />-   VBScript: `String`|Flag to enable or disable the client agent.|  
|`siteCode`<br /><br /> `siteToChange`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 System.Collections.Generic  

 System.ComponentModel  

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
 [Configuration Manager Software Distribution](../../../../develop/core/servers/configure/software-distribution.md)   
 [Software Distribution Setup and Configuration](../../../../develop/core/servers/configure/software-distribution-setup-and-configuration.md)   
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)
