---
title: "Lazy Properties by Using Managed Code"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 8a958d91-c654-4f11-a9e4-387dc998c2ee
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# How to Read Lazy Properties by Using Managed Code
To read a lazy property from a Configuration Manager object returned in a query, you get the object instance, which retrieves any lazy object properties from the SMS Provider.  

> [!NOTE]
>  If you know the full path to the WMI object, a call to the [GetInstance](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.connectionmanagerbase.getinstance.aspx) method returns the WMI object along with any lazy properties. For more information, see [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md).  

 For more information, see [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md).  

### To read lazy properties  

1.  Set up a connection to the SMS Provider. For more information, see [How to Connect to an SMS Provider in Configuration Manager by Using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md).  

2.  Use **QueryProcessor** object to query Configuration Manager objects.  

3.  Iterate through the query results.  

4.  Using the **WqlConnectionManager** you obtain in step one, call [GetInstance](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.connectionmanagerbase.getinstance.aspx) to get the [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) object for each queried object that you want to get lazy properties from.  

## Example  
 The following C# code example queries for all [SMS_Collection](../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md) objects and then displays rule names obtained from the `CollectionRules` lazy property.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```  
public void ReadLazyProperty(WqlConnectionManager connection)  
{  
    try  
    {  
        // Query all collections.  
        IResultObject collections = connection.QueryProcessor.ExecuteQuery("Select * from SMS_Collection");  
        foreach (IResultObject collection in collections)  
        {  
            // Get the collection object and lazy properties.  
            collection.Get();  

            Console.WriteLine(collection["Name"].StringValue);  

            // Get the rules.  
            List<IResultObject> rules = collection.GetArrayItems("CollectionRules");  
            if (rules.Count == 0)  
            {  
                Console.WriteLine("No rules");  
                Console.WriteLine();  
                continue;  
            }  

            foreach (IResultObject rule in rules)  
            {  
                // Display rule names.  
                Console.WriteLine("Rule name: " + rule["RuleName"].StringValue);  
            }  

            Console.WriteLine();  
        }  
    }  
    catch (SmsQueryException ex)  
    {  
        Console.WriteLine("Failed to get collection. Error: " + ex.Message);  
        throw;  
    }  
}  

```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   `WqlConnectionManager`|A valid connection to the SMS Provider.|  

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
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsconnectionexception.aspx) and [SmsQueryException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsqueryexception.aspx). These can be caught together with [SmsException](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsexception.aspx).  

## See Also  
 [Objects overview](configuration-manager-objects-overview.md)
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [How to Call a Configuration Manager Object Class Method by Using Managed Code](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-managed-code.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)   
