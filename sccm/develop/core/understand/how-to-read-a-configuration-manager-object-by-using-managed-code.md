---
title: "How to Read a Configuration Manager Object by Using Managed Code"
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
ms.assetid: c02c7824-d46e-4a7a-b96d-8d1aa695fbbc
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Read a Configuration Manager Object by Using Managed Code
To read a System Center Configuration Manager object instance by using the managed SMS Provider, use [WqlConnectionManager.GetInstance](assetId:///WqlConnectionManager.GetInstance?qualifyHint=False&autoUpgrade=True). The <xref:Microsoft.ConfigurationManagement.ManagementProvider.ConnectionManagerBase.GetInstance*> method takes a string that identifies a specific object instance and returns an <xref:Microsoft.ConfigurationManagement.ManagementProvider.IResultObject> object that is used to access the object.  
  
 The following example function shows the name and description for a supplied package identifier.  
  
### To read a Configuration Manager object  
  
1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../develop/core/understand/2a435561-01b7-45d5-b7cf-89fc1845025f.md).  
  
2.  Call [WqlConnectionManager](assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True) class [GetInstance](assetId:///GetInstance?qualifyHint=False&autoUpgrade=True) method to get the [IResultObject](assetId:///IResultObject?qualifyHint=False&autoUpgrade=True) object for the object you want.  
  
3.  Display the properties of the assetId:///IResultObject?qualifyHint=False&autoUpgrade=True.  
  
## Example  
 The following code example shows how to read a Configuration Manager object.  
  
 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling code snippets.md).  
  
```  
public void DisplayPackageName(WqlConnectionManager connection, string packageID)  
{  
    try   
    {  
        // Get the package.  
        IResultObject package = connection.GetInstance(@"SMS_Package.PackageID='" + packageID + "'");  
        Console.WriteLine("Package Name: " + package["Name"].StringValue);  
        Console.WriteLine("Package Description: " + package["Description"].StringValue);  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to get package. Error: " + ex.Message);  
        throw;  
    }  
}  
  
```  
  
 This example method has the following parameters:  
  
|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`Connection`|-   Managed: assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True|-   A valid connection to the SMS Provider.|  
|`PackageID`|-   Managed: `String`|A valid package identifier. Obtained from the [SMS_Package](assetId:///SMS_Package?qualifyHint=False&autoUpgrade=True) class [PackageID](assetId:///PackageID?qualifyHint=False&autoUpgrade=True) property.|  
  
## Compiling the Code  
  
### Namespaces  
 System  
  
 System.Collections.Generic  
  
 System.ComponentModel  
  
 Microsoft.ConfigurationManagement.ManagementProvider  
  
 Microsoft.ConfigurationManagement.ManagementProvider.WqlQueryEngine  
  
### Assembly  
 microsoft.configurationmanagement.managementprovider  
  
 adminui.wqlqueryengine  
  
## Robust Programming  
 The Configuration Manager exceptions that can be raised are <xref:Microsoft.ConfigurationManagement.ManagementProvider.SmsConnectionException> and <xref:Microsoft.ConfigurationManagement.ManagementProvider.SmsQueryException>. These can be caught together with <xref:Microsoft.ConfigurationManagement.ManagementProvider.SmsException>.  
  
## See Also  
 [About Configuration Manager Objects](../../../develop/core/understand/about-configuration-manager-objects.md)   
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [How to Call a Configuration Manager Object Class Method by Using Managed Code](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/2a435561-01b7-45d5-b7cf-89fc1845025f.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/cfbb34e8-9b47-48db-a8ef-408a0a89ad17.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read Lazy Properties by Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)