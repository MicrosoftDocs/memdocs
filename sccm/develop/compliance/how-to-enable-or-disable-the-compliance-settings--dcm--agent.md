---
title: "Enable or Disable the Compliance Settings Agent"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: bcb099cd-4433-4223-bb2e-23fdfd32fb41
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Enable or Disable the Compliance Settings (DCM) Agent
In System Center Configuration Manager, you enable or disable the Desired Configuration Management Client Agent by modifying the site control file settings.  

### To enable or disable the Desired Configuration Management Client Agent  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Desired Configuration Management Client Agent section of the site control file by using the [SMS_SCI_ClientComp](../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the changes to the site control file.  

## Example  
 The following example method enables or disables the Desired Configuration Management Client Agent by using the [SMS_SCI_ClientComp](../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class to connect to the site control file and change the `Flag` property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub EnableDisableDCMClientAgent(swbemServices,   _   
                                swbemContext,    _  
                                siteCode,        _  
                                enableDisableFlag)  

' Load site control file and get DCM client component section.  
swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  
Set swbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteCode & "',ItemName='Configuration Management Agent'", , swbemContext)  

' Display DCM client agent settings before change.  
Wscript.Echo " "  
Wscript.Echo "Properties - Before Change"  
Wscript.Echo "---------------------------"  
Wscript.Echo swbemInst.ClientComponentName  
Wscript.Echo swbemInst.Flags & " (0 = Disabled, 1 = Enabled)"  

' Set DCM client agent by setting flags value to  0 or 1 using the enableDisableFlag variable.  
swbemInst.Flags = enableDisableFlag  

' Save new client agent settings.  
swbemInst.Put_ , swbemContext  
swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Commit", , , swbemContext  
Set swbemInst = Nothing  

' Refresh in-memory copy of the site control file and get the DCM client component section.  
swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  
Set swbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteCode & "',ItemName='Configuration Management Agent'", , swbemContext)  

' Display DCM client agent settings after change.  
Wscript.Echo " "  
Wscript.Echo "Properties - After Change"  
Wscript.Echo "---------------------------"  
Wscript.Echo swbemInst.ClientComponentName  
Wscript.Echo swbemInst.Flags & " (0 = Disabled, 1 = Enabled)"  

Set swbemInst = Nothing  

End Sub  

```  

```c#  

public void EnableDisableDCMClientAgent(WqlConnectionManager connection,  
                                        string siteCode,  
                                        string enableDisableFlag)  
{  

    try  
    {  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Configuration Management Agent'");  

        // Display DCM client agent settings before change.  
        Console.WriteLine();  
        Console.WriteLine("Properties - Before Change");  
        Console.WriteLine("---------------------------");  
        Console.WriteLine(siteDefinition["ClientComponentName"].StringValue);  
        Console.WriteLine(siteDefinition["Flags"].StringValue + " (0 = Disabled, 1 = Enabled)");  

        // Set DCM client agent by setting flags value to  0 or 1 using the enableDisableFlag variable.  
        siteDefinition["Flags"].StringValue = enableDisableFlag;  

        // Save the settings.  
        siteDefinition.Put();  

        // Verify change by reconnecting and getting the value again.  
        IResultObject siteDefinition2 = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Configuration Management Agent'");  

        // Display DCM client agent settings after change.  
        Console.WriteLine();  
        Console.WriteLine("Properties - After Change");  
        Console.WriteLine("--------------------------");  
        Console.WriteLine(siteDefinition2["ClientComponentName"].StringValue);  
        Console.WriteLine(siteDefinition2["Flags"].StringValue + " (0 = Disabled, 1 = Enabled)");  

    }  

    catch (SmsException eX)  
    {  
        Console.WriteLine("Failed. Error: " + eX.InnerException.Message);  
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
|`enableDisableFlag`|-   Managed: `String`<br />-   VBScript: `String`|Determines whether the Desired Configuration Management Client Agent is enabled or disabled.<br /><br /> 0 - disabled<br /><br /> 1 - enabled|  

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
 [About Compliance Settings (DCM) Setup and Configuration](../../develop/compliance/about-compliance-settings--dcm--setup-and-configuration.md)   
 [About the Configuration Manager Site Control File](../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_ClientComp Server WMI Class](../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md)
