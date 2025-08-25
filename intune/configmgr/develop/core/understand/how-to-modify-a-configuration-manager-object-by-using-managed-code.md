---
title: Modify an Object by Using Managed Code
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: how-to
ms.assetid: ebb14714-c951-479e-9fad-dd2d7a32e739
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
description: Learn how to modify a configuration manager object by using managed code with the provided examples and links.
ms.reviewer: mstewart
---
# How to Modify a Configuration Manager Object by Using Managed Code
To modify a Configuration Manager object instance by using the managed SMS Provider, use the object's [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) interface to make modifications. You then call the [IResultObject.Put](/previous-versions/system-center/developer/cc146500(v=msdn.10)) method to submit the changes.

> [!NOTE]
>  The IResultObject interface for an object can be obtained through the WqlConnectionManager.GetInstance method or through other queries. For an example that uses asynchronous queries, see [How to Perform an Asynchronous Configuration Manager Query Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md).

### To modify a Configuration Manager object

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md).

2.  Using the **WqlConnectionManager** object you obtain in step one, call *GetInstance* to get an [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) for the required object.

3.  Make changes to object using the IResultObject.

4.  Commit the changes to the SMS provider with the IResultObject object [Put](/previous-versions/system-center/developer/cc146500(v=msdn.10)) method.

## Example
 The following example function updates a package's description from a supplied package identifier and description.

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).

```

public void ModifyPackageDescription(WqlConnectionManager connection, string packageID, string description)
{
    try
    {
        IResultObject package = connection.GetInstance(@"SMS_Package.PackageID='" + packageID + "'");
        Console.WriteLine("Package Name: " + package["Name"].StringValue);
        Console.WriteLine("Current Description: " + package["Description"].StringValue);

        package["Description"].StringValue = description;

        package.Put();

        Console.WriteLine("New description: " + package["Description"].StringValue);
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
|`connection`|`WqlConnectionManager`|A valid connection to the SMS Provider.|

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
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)
 [How to Read Lazy Properties by Using Managed Code](../../../develop/core/understand/how-to-read-lazy-properties-by-using-managed-code.md)
