---
title: "Delete a Driver Package"
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
ms.assetid: 74397fd4-f479-44d9-9400-b45ab32f07c7searchScope: - ConfigMgr SDK
caps.latest.revision: 9
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete a Driver Package in Configuration Manager
You delete an operating system deployment driver package, in System Center Configuration Manager, by deleting its [SMS_DriverPackage](../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) object.  

> [!NOTE]
>  Windows drivers that are referenced by the driver package are not deleted.  

### To delete a driver package  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Get the [SMS_DriverPackage](../../develop/reference/osd/sms_driverpackage-server-wmi-class.md) object for the driver that you want to delete.  

3.  Delete the SMS_DriverPackage object.  

## Example  
 The following example method deletes a driver package identified by its package identifier.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../develop/core/understand/calling-code-snippets.md).  

```vbs  
Sub DeleteDriverPackage(connection,packageID)  

        ' Get the driver.  
        Set driverPackage = connection.Get("SMS_DriverPackage.PackageID='" & packageID & "'")  

        ' Delete the driver package.  
        driverPackage.Delete_  

End Sub  
```  

```c#  
public void DeleteDriverPackage(  
    WqlConnectionManager connection,   
    string packageId)  
{  
    try  
    {  
        // Get the driver package.  
        IResultObject driverPackage = connection.GetInstance("SMS_DriverPackage.packageId='" + packageId + "'");  

        // Delete the driver package.  
        driverPackage.Delete();  
    }  
    catch (SmsException e)  
    {  
        Console.WriteLine("Failed to delete driver package: " + e.Message);  
        throw;  
    }  
}  
```  

 The example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed:`WqlConnectionManager`<br />-   VBScript: [SWbemServices](https://msdn.microsoft.com/library/aa393854.aspx)|A valid connection to the SMS Provider.|  
|`packageID`|-   Managed: `String`<br />-   VBScript: `String`|-   The driver package identifier available in SMS_DriverDriverPackage.PackageID.|  

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

## Robust Programming  
 For more information about error handling, see [About Configuration Manager Errors](../../develop/core/understand/about-configuration-manager-errors.md).  

## .NET Framework Security  
 For more information about securing Configuration Manager applications, see [Securing Configuration Manager Applications](../../develop/core/understand/securing-configuration-manager-applications.md).  

## See Also  
 [Operating System Deployment Driver Management](../../develop/osd/operating-system-deployment-driver-management.md)
