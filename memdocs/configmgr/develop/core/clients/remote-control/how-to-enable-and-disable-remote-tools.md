---
title: "Enable and Disable Remote Tools"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: bc7ee810-933e-403f-af2d-da75f4c17c1c
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# How to Enable and Disable Remote Tools
You enable or disable the Remote Tools Client Agent, in Configuration Manager, by modifying the site control file settings.  

### To enable or disable the Remote Tools Client Agent  

1.  Set up a connection to the SMS Provider.  

2.  Make a connection to the Remote Tools Client Agent section of the site control file by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class.  

3.  Loop through the array of available properties, making changes as needed.  

4.  Commit the changes to the site control file.  

## Example  
 The following example method enables or disables the Remote Tools Client Agent by using the [SMS_SCI_ClientComp](../../../../develop/reference/core/servers/configure/sms_sci_clientcomp-server-wmi-class.md) class to connect to the site control file and change properties.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub EnableDisableRemoteControlClientAgent(swbemServices,   _  
                                          swbemContext,    _  
                                          siteCode,    _  
                                          enableDisableClientAgent)  

    ' Load site control file and get client component section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  
    Set objSWbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteCode & "',ItemName='Remote Control'", , swbemContext)  

    ' Display client agent settings before change.  
    Wscript.Echo " "  
    Wscript.Echo "Properties - Before Change"  
    Wscript.Echo "---------------------------"  
    Wscript.Echo objSWbemInst.ClientComponentName  
    Wscript.Echo objSWbemInst.Flags & " (0 = Disabled, 1 = Enabled)"  

    ' Set the client agent by setting the Flags value to 0 or 1 using the enableDisableClientAgent variable.  
    objSWbemInst.Flags = enableDisableClientAgent  

    ' Save the new client agent settings.  
    objSWbemInst.Put_ , swbemContext  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Commit", , , swbemContext  

    ' Refresh the in-memory copy of the site control file and get the client component section.  
    swbemServices.ExecMethod "SMS_SiteControlFile.Filetype=1,Sitecode=""" & siteCode & """", "Refresh", , , swbemContext  
    Set objSWbemInst = swbemServices.Get("SMS_SCI_ClientComp.Filetype=1,Itemtype='Client Component',Sitecode='" & siteCode & "',ItemName='Remote Control'", , swbemContext)  

    ' Display the client agent settings after the change.  
    Wscript.Echo " "  
    Wscript.Echo "Properties - After Change"  
    Wscript.Echo "---------------------------"  
    Wscript.Echo objSWbemInst.ClientComponentName  
    Wscript.Echo objSWbemInst.Flags & " (0 = Disabled, 1 = Enabled)"  

End Sub  

```  

```c#  

public void EnableDisableRemoteControlClientAgent(WqlConnectionManager connection,  
                                                  string siteCode,  
                                                  string enableDisableClientAgent)  
{  
    try  
    {  
        IResultObject siteDefinition = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Remote Control'");  

        // Display Remote Control client agent settings before changing the properties.  
        Console.WriteLine();  
        Console.WriteLine("Properties - Before Change");  
        Console.WriteLine("---------------------------");  
        Console.WriteLine(siteDefinition["ClientComponentName"].StringValue);  
        Console.WriteLine(siteDefinition["Flags"].StringValue + " (0 = Disabled, 1 = Enabled)");  

        // Set Remote Control client agent by setting "Flags" value to 0 or 1 by using the enableDisableClientAgent variable.  
        siteDefinition["Flags"].StringValue = enableDisableClientAgent;  

        // Save the settings.  
        siteDefinition.Put();  

        // Verify the change by reconnecting and getting the value again.  
        IResultObject siteDefinition2 = connection.GetInstance(@"SMS_SCI_ClientComp.FileType=1,ItemType='Client Component',SiteCode='" + siteCode + "',ItemName='Remote Control'");  

        // Display Remote Control client agent settings after changing the properties.  
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

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|Parameter|Type|Description|  
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`swbemContext`|-   VBScript: `SWbemContext`|A valid context object. For more information, see [How to Add a Configuration Manager Context Qualifier by Using WMI](../../../../develop/core/understand/how-to-add-a-configuration-manager-context-qualifier-by-using-wmi.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`enableDisableClientAgent`|-   Managed: `String`<br />-   VBScript: `String`|Determines whether the Remote Tools client agent is enabled or disabled.<br /><br /> -   0 - Disabled<br />-   1 - Enabled|  

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
 [Configuration Manager Software Development Kit](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)