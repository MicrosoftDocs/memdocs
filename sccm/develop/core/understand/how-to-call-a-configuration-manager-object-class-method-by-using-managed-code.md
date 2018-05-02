---
title: "Call an Object Class Method by Using Managed Code"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 46cb95e6-9dae-4c08-9cfb-1a570e4c05bc
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to Call a Configuration Manager Object Class Method by Using Managed Code
To call a SMS Provider class method, in System Center Configuration Manager, you use the [ExecuteMethod](https://msdn.microsoft.com/en-us/library/cc146186.aspx) method. You populate a [Dictionary](https://msdn.microsoft.com/library/aa239680.aspx) object with the method's parameters, and the return value is an [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) object that contains the result of the method call.  

> [!NOTE]
>  To call a method on an object instance, use the [ExecuteMethod](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.executemethod.aspx) method on the [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) object instance.  

### To call a Configuration Manager object class method  

1.  Set up a connection to the SMS Provider. For more information, see [About the SMS Provider in Configuration Manager](../../../develop/core/understand/about-the-sms-provider-in-configuration-manager.md).  

2.  Create the input parameters as a **Dictionary** object.  

3.  Using the **WqlConnectionManager** object instance, call [ExecuteMethod](https://msdn.microsoft.com/en-us/library/cc146186.aspx) and specify the class name and input parameters.  

4.  Retrieve the method return value from the *ReturnValue* property in the returned **IResultObject** object.  

## Example  
 The following example validates a collection rule query by calling the [SMS_CollectionRuleQuery](../../../develop/reference/core/clients/collections/sms_collectionrulequery-server-wmi-class.md) class [ValidateQuery](../../../develop/reference/core/clients/collections/validatequery-method-in-class-sms_collectionrulequery.md) class method.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```  
public void ValidateQueryRule(WqlConnectionManager connection, string wqlQuery)  
{  
    try  
    {  
        Dictionary<string,object> validateQueryParameters = new Dictionary<string,object>();  

        // Add the sql query as the WQLQuery parameter.  
        validateQueryParameters.Add("WQLQuery",wqlQuery);  

        // Call the method  
        IResultObject result=connection.ExecuteMethod("SMS_CollectionRuleQuery", "ValidateQuery", validateQueryParameters);  

        if (result["ReturnValue"].BooleanValue == true)  
        {  
            Console.WriteLine (wqlQuery + " is a valid query");  
        }  
        else  
        {  
            Console.WriteLine (wqlQuery + " is not a valid query");  
        }  
     }  
     catch (SmsException ex)  
     {  
           Console.WriteLine("Failed to validate query rule: ",ex.Message);  
           throw;  
     }  
}  

```  

 This example method has the following parameters:  

|Parameter|Type|Description|  
|---------------|----------|-----------------|  
|`connection`|-   Managed: **WqlConnectionManager**|A valid connection to the SMS Provider.|  
|`wqlQuery`|-   Managed: **IResultObject**|A WQL query string. For this example, `SELECT * FROM SMS_R_System` is a valid query.|  

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
 [About Configuration Manager Objects](../../../develop/core/understand/about-configuration-manager-objects.md)   
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Use Configuration Manager Objects With Managed Code](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-managed-code.md)
