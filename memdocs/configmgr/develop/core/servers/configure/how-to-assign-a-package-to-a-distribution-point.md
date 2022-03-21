---
title: "Assign a Package to a Distribution Point"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: e6b6bb80-6c63-4bc0-9f7e-8f8194e281e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Assign a Package to a Distribution Point
The following example shows how to assign a distribution point to a package by using the `SMS_DistributionPoint` and `SMS_SystemResourceList` classes in Configuration Manager. You only need to assign a distribution point to a package if the package contains source files (PkgSourcePath). The package is not advertised until the program source files have been propagated to a distribution point share. You can use the default distribution point share, or you can specify a share to use. You can also specify more than one distribution point to use to distribute your package source files, although this example does not demonstrate that.  

### To assign a package to a distribution point  

1.  Set up a connection to the SMS Provider.  

2.  Create a new distribution point object (this is not an actual distribution point).  

3.  Associate the existing package with the new distribution point object.  

4.  Query for a single distribution point based on the provided site code and server name.  

5.  Use the query results to populate the `ServerNALPath` property of the distribution point object.  

6.  Save the distribution point object and properties.  

## Example  
 The following example method assigns a package to a distribution point.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub SWDAssignPackageToDistributionPoint(connection, existingPackageID, siteCode, serverName)  

    Const wbemFlagReturnImmediately = 16  
    Const wbemFlagForwardOnly = 32  
    Dim distributionPoint  
    Dim query  
    Dim listOfResources  
    Dim resource  

    ' Create distribution point object (this is not an actual distribution point).  
    Set distributionPoint = connection.Get("SMS_DistributionPoint").SpawnInstance_  

    ' Associate the existing package with the new distribution point object.  
    distributionPoint.PackageID = existingPackageID       

    ' This query selects a single distribution point based on the provided SiteCode and ServerName.  
    query = "SELECT * FROM SMS_SystemResourceList WHERE RoleName='SMS Distribution Point' AND SiteCode='" & siteCode & "' AND ServerName='" & serverName & "'"  

    Set listOfResources = connection.ExecQuery(query, , wbemFlagForwardOnly Or wbemFlagReturnImmediately)  

    ' The query returns a collection that needs to be enumerated (although we should only get one instance back).  
    For Each resource In ListOfResources        
        distributionPoint.ServerNALPath = Resource.NALPath  
        distributionPoint.SiteCode = Resource.SiteCode          
    Next  

    ' Save the distribution point instance for the package.  
    distributionPoint.Put_   

    ' Display notification text.  
    Wscript.Echo "Assigned package: " & distributionPoint.PackageID   

End Sub  
```  

```c#  
public void AssignPackageToDistributionPoint(WqlConnectionManager connection, string existingPackageID, string siteCode, string serverName)  
{  
    try  
    {  
        // Create the distribution point object (this is not an actual distribution point).  
        IResultObject distributionPoint = connection.CreateInstance("SMS_DistributionPoint");  

        // Associate the package with the new distribution point object.   
        distributionPoint["PackageID"].StringValue = existingPackageID;  

        // This query selects a single distribution point based on the provided siteCode and serverName.  
        string query = "SELECT * FROM SMS_SystemResourceList WHERE RoleName='SMS Distribution Point' AND SiteCode='" + siteCode + "' AND ServerName='" + serverName + "'";  

        //   
        IResultObject listOfResources = connection.QueryProcessor.ExecuteQuery(query);  
        foreach (IResultObject resource in listOfResources)  
        {  
            Console.WriteLine(resource["SiteCode"].StringValue);  
            distributionPoint["ServerNALPath"].StringValue = resource["NALPath"].StringValue;  
            distributionPoint["SiteCode"].StringValue = resource["SiteCode"].StringValue;  
        }  

        // Save the distribution point object and properties.  
        distributionPoint.Put();  

        // Output package ID of assigned package.  
        Console.WriteLine("Assigned package: " + distributionPoint["PackageID"].StringValue);  
    }  

    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create package. Error: " + ex.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`<br /><br /> `swbemServices`|-   Managed: `WqlConnectionManager`<br />-   VBScript: [SWbemServices](/windows/win32/wmisdk/swbemservices)|A valid connection to the SMS Provider.|  
|`existingPackageID`|-   Managed: `String`<br />-   VBScript: `String`|The ID of the existing package.|  
|`siteCode`|-   Managed: `String`<br />-   VBScript: `String`|The site code.|  
|`serverName`|-   Managed: `String`<br />-   VBScript: `String`|The name of the server.|  

## Compiling the Code  
 The C# example requires:  

### Namespaces  
 System  

 Microsoft.ConfigurationManagement.ManagementProvider  

 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  

### Assembly  
 adminui.wqlqueryengine  

 microsoft.configurationmanagement.managementprovider  

 mscorlib  

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../../../develop/core/understand/about-configuration-manager-errors.md).  

## See Also  
 [Software distribution overview](software-distribution-overview.md)
 [About the site control file](../../understand/about-the-configuration-manager-site-control-file.md)
 [SMS_SCI_Component Server WMI Class](../../../../develop/reference/core/servers/configure/sms_sci_component-server-wmi-class.md)   
 [SMS_SystemResourceList Server WMI Class](../../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md)
