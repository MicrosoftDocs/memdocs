---
title: "How to Create a Configuration Manager Object by Using Managed Code"
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
ms.assetid: 2c6984bf-f2be-4e07-8c7c-579928d02cac
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a Configuration Manager Object by Using Managed Code
To create a System Center Configuration Manager object by using the managed SMS Provider, use [WqlConnectionManager.CreateInstance](assetId:///WqlConnectionManager.CreateInstance?qualifyHint=False&autoUpgrade=True) method. The <xref:Microsoft.ConfigurationManagement.ManagementProvider.ConnectionManagerBase.CreateInstance*> method takes the required object type as a string parameter and returns an <xref:Microsoft.ConfigurationManagement.ManagementProvider.IResultObject> object that is used to populate the new object. The [IResultObject.Put](assetId:///IResultObject.Put?qualifyHint=False&autoUpgrade=True) method must be called to submit the object to the SMS Provider.  
  
### To create a Configuration Manager object  
  
1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  
  
2.  Using the [WqlConnectionManager](assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True) connection object you obtain in step one, call [CreateInstance](assetId:///CreateInstance?qualifyHint=False&autoUpgrade=True) to create the required the WMI object, and receive its IResultObject object instance.  
  
3.  Populate the <xref:Microsoft.ConfigurationManagement.ManagementProvider.IResultObject> properties.  
  
4.  Commit the <xref:Microsoft.ConfigurationManagement.ManagementProvider.IResultObject> to the SMS Provider.  
  
## Example  
 The following example demonstrates how to create and then populate a new Configuration Manager package (`SMS_Package`).  
  
 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling code snippets.md).  
  
```  
public void CreatePackage(WqlConnectionManager connection)  
{  
    try  
    {  
        IResultObject package = connection.CreateInstance("SMS_Package");  
        package["Name"].StringValue = "Test Package";  
        package["Description"].StringValue = "A test package";  
        package["PkgSourcePath"].StringValue = @"c:\Package Source";  
  
        package.Put();  
    }  
  
    catch (SmsException ex)  
    {  
        Console.WriteLine("Failed to create package. Error: " + ex.Message);  
        throw;  
    }  
}  
  
```  
  
 This example method has the following parameters:  
  
|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|Managed: assetId:///WqlConnectionManager?qualifyHint=False&autoUpgrade=True|A valid connection to the SMS Provider.|  
  
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
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/cfbb34e8-9b47-48db-a8ef-408a0a89ad17.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Read Lazy Properties by Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)