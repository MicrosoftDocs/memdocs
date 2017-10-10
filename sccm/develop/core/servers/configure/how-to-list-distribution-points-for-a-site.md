---
title: "List Distribution Points for a Site"
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
ms.assetid: f70395dc-3266-4406-8189-2d741c746528searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to List Distribution Points for a Site
The following example shows how to assign a distribution point to a package by using the [SMS_DistributionPoint Server WMI Class](../../../../develop/reference/core/servers/configure/sms_distributionpoint-server-wmi-class.md) class and class properties in System Center Configuration Manager.  

 You only need to assign a distribution point to a package if the package contains source files. The package is not advertised until the program source files have been propagated to a distribution point share. You can use the default distribution point share, or you can specify a share to use. You can also specify more than one distribution point to use to distribute your package source files, although the following example does not demonstrate that.  

> [!NOTE]
>  To identify branch distribution points, check the [IsPeerDP](../../../../develop/reference/core/servers/configure/sms_distributionpoint-server-wmi-class.md) property of the specific [SMS_DistributionPoint](../../../../develop/reference/core/servers/configure/sms_distributionpoint-server-wmi-class.md) class instance. If the IsPeerDP property is true, then the distribution point is a branch distribution point.  

### To list distribution points for a site  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Run a query, which populates a variable with a collection of distribution point objects.  

3.  Enumerate through the collection of and list the distribution points returned by the query.  

## Example  
 The following example method lists distribution points for a site.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ListDistributionPointsForSite(connection, siteCode)  

    ' This query selects all distribution points for a site based on the provided site code.      
    Query = "SELECT * FROM SMS_SystemResourceList WHERE RoleName='SMS Distribution Point' AND SiteCode='" & siteCode & "'"  

    ' Run query, which populates listOfResources with a collection of objects.  
    Set ListOfResources = connection.ExecQuery(query, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' Output header for list of distribution points.  
    Wscript.Echo "List of distribution points for site: " & siteCode  
    Wscript.Echo "--------------------------------------------"  

    ' Enumerate through the collection of objects returned by the query.  
    For Each resource In listOfResources        
        ' Output the server name for each distribution point.  
        Wscript.Echo resource.ServerName  
    Next  

End Sub  
```  

```c#  
public void ListDistributionPointsForSite(WqlConnectionManager connection, string siteCode)  
{  
    try  
    {  
        // This query selects all distribution points for a site based on the provided site code.  
        string query = "SELECT * FROM SMS_SystemResourceList WHERE RoleName='SMS Distribution Point' AND SiteCode='" + siteCode + "'";  

        // Run query, which populates 'listOfResources' with a collection of objects.   
        IResultObject listOfResources = connection.QueryProcessor.ExecuteQuery(query);  

        // Output header for list of distribution points.  
        Console.WriteLine("List of distribution points for site: " + siteCode);  
        Console.WriteLine("--------------------------------------------");  

        // Enumerate through the collection of objects returned by the query.  
        foreach (IResultObject resource in listOfResources)  
        {  
            // Output the server name for each distribution point.  
            Console.WriteLine(resource["ServerName"].StringValue);  
        }  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to list distribution points. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swebemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code for the site that supports the distribution points.|  

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
 [Distribution Points](../../../../develop/core/servers/configure/distribution-points.md)   
 [About the Configuration Manager Site Control File](../../../../develop/core/understand/about-the-configuration-manager-site-control-file.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using Managed Code](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-managed-code.md)   
 [How to Read and Write to the Configuration Manager Site Control File by Using WMI](../../../../develop/core/understand/how-to-read-and-write-to-the-site-control-file-by-using-wmi.md)   
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [SMS_DistributionPoint Server WMI Class](../../../../develop/reference/core/servers/configure/sms_distributionpoint-server-wmi-class.md)
