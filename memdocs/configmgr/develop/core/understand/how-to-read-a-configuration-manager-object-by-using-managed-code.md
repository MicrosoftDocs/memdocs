---
title: "Read an Object by Using Managed Code"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: c02c7824-d46e-4a7a-b96d-8d1aa695fbbc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Read a Configuration Manager Object by Using Managed Code
To read a Configuration Manager object instance by using the managed SMS Provider, use *WqlConnectionManager.GetInstance*. The [GetInstance](/previous-versions/system-center/developer/cc146190(v=msdn.10)) method takes a string that identifies a specific object instance and returns an [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) object that is used to access the object.  

 The following example function shows the name and description for a supplied package identifier.  

### To read a Configuration Manager object  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md).  

2.  Call WqlConnectionManager class [GetInstance](/previous-versions/system-center/developer/cc146190(v=msdn.10)) method to get the [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) object for the object you want.  

3.  Display the properties of the [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)).  

## Example  
 The following code example shows how to read a Configuration Manager object.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

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
|`Connection`|-   Managed: `WqlConnectionManager`|-   A valid connection to the SMS Provider.|  
|`PackageID`|-   Managed: `String`|A valid package identifier. Obtained from the [SMS_Package](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md) class PackageID property.|  

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
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) and [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)). These can be caught together with [SmsException](/previous-versions/system-center/developer/cc147433(v=msdn.10)).  

## See Also  
 [Objects overview](configuration-manager-objects-overview.md)
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [How to Call a Configuration Manager Object Class Method by Using Managed Code](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read Lazy Properties by Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)
