---
title: "Determine the Health of a Site"
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
ms.assetid: 2b49a2b8-b141-4ed3-9b94-925a6cca1711searchScope: - ConfigMgr SDK
caps.latest.revision: 8
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Determine the Health of a Configuration Manager Site
You can determine the overall health or status of a site, in System Center Configuration Manager, by inspecting the `SMS_SummarizerSiteStatus` object `Status` property. The `Status` property has three possible values:  

|Value|Description|  
|-----------|-----------------|  
|0|The site is healthy.|  
|1|The site has warning conditions.|  
|2|The site has error conditions.|  

 `SMS_SummarizerSiteStatus` is an example of a System Center Configuration Manager summarizer. For more information about other summarizer classes, see [Status Server WMI Classes](../../../../develop/reference/core/servers/manage/status-server-wmi-classes.md).  

### To determine a site's health  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the `SMS_SummarizerSiteStatus` object by using the Configuration Manager site code.  

3.  Inspect the `SMS_SummarizerSiteStatus` object `Status` property to determine the site status  

## Example  
 The following example determines the health of the site code supplied in the parameter `siteCode`.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub ShowSiteHealth(connection, siteCode)  

    Dim siteHealth  
    Dim health  

    On Error Resume Next   

    ' Get the site status summarizer.  
    Set siteHealth = connection.Get("SMS_SummarizerSiteStatus.SiteCode='" & siteCode & "'")  
    If Err.Number<>0 Then  
        Wscript.Echo "Couldn't get site health"  
        Exit Sub  
    End If  

    ' Display the site health.  
    health="Health for site " + siteCode + " "  

    Select Case siteHealth.Status  
        Case 0  
            heath = health + "is OK"  
        Case 1  
            health = health + "has warnings"  
        Case 2  
            health = health + "is critical"  
        Case Else  
            health = health + "is not known"  
    End Select          

    Wscript.Echo health  
End Sub  
```  

```c#  
public void ShowSiteHealth(WqlConnectionManager connection, string siteCode)  
{  
    try  
    {  
        IResultObject siteHealth = connection.GetInstance(@"SMS_SummarizerSiteStatus.SiteCode='" + siteCode + "'");  

        Console.Write("Health for site {0}", siteCode);  
        switch (siteHealth["Status"].IntegerValue)  
        {  
            case 0:  
                Console.WriteLine("is OK");  
                break;  
            case 1:  
                Console.WriteLine("has warnings");  
                break;  
            case 2:  
                Console.WriteLine("is critical");  
                break;  
            default:  
                Console.WriteLine("is not known");  
                break;  
        }  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to show site status: " + e.Message);  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: [WqlConnectionManager](assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True)<br />-   VBScript: [SWbemServices](assetId:///SWbemServices?qualifyHint=False&autoUpgrade=True)|A valid connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|A valid task System Center Configuration Manager site code|  

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
 [About Configuration Manager Status and State](../../../../develop/core/servers/manage/about-configuration-manager-status-and-summarizers.md)   
 [Status Server WMI Classes](../../../../develop/reference/core/servers/manage/status-server-wmi-classes.md)
