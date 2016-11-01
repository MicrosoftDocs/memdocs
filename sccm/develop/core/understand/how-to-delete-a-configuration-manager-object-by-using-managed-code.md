---
title: "How to Delete a Configuration Manager Object by Using Managed Code"
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
ms.assetid: 3e797ee7-ebc6-4d4d-b5d7-8a3b901d8d51
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Delete a Configuration Manager Object by Using Managed Code
To delete a System Center Configuration Manager object by using the managed SMS Provider, use the [IResultObject.Delete](assetId:///IResultObject.Delete?qualifyHint=False&autoUpgrade=True) method. You can get a <xref:Microsoft.ConfigurationManagement.ManagementProvider.IResultObject> object for a System Center Configuration Manager object in numerous ways. For more information, see [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)  
  
### To delete a Configuration Manager object  
  
1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  
  
2.  Using the `WqlConnectionManager` object you obtain in step one, call  the `GetInstance` method to get the `IResultObject` object for the Configuration Manager object.  
  
3.  Call the [IResultObject](assetId:///IResultObject?qualifyHint=False&autoUpgrade=True) object [Delete](assetId:///Delete?qualifyHint=False&autoUpgrade=True) method to delete the Configuration Manager object.  
  
## Example  
 The following example deletes a package by using the supplied package identifier. This example uses the [WqlConnectionManager](assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True) class [GetInstance](assetId:///GetInstance?qualifyHint=False&autoUpgrade=True) method to get an assetId:///IResultObject?qualifyHint=False&autoUpgrade=True object for the Configuration Manager package and then deletes the package.  
  
 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling code snippets.md).  
  
```  
public void DeletePackage(WqlConnectionManager connection, string packageID)  
{  
    try  
    {  
        IResultObject package = connection.GetInstance(@"SMS_Package.PackageID='" + packageID + "'");  
        package.Delete();  
    }  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to delete package: " + ex.Message);  
        throw;  
    }  
}  
  
```  
  
 This example method has the following parameters:  
  
|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True|A valid connection to the SMS Provider.|  
|`PackageID`|-   `String`|The package identifier for an existing package. This can be obtained from the [SMS_Package](assetId:///SMS_Package?qualifyHint=False&autoUpgrade=True) class [PackageID](assetId:///PackageID?qualifyHint=False&autoUpgrade=True) property.|  
  
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
 [How to Call a Configuration Manager Object Class Method by Using Managed Code](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/2a435561-01b7-45d5-b7cf-89fc1845025f.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/cfbb34e8-9b47-48db-a8ef-408a0a89ad17.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Read Lazy Properties by Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)