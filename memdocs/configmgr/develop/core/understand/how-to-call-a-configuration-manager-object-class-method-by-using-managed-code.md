---
title: "Call an Object Class Method by Using Managed Code"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 46cb95e6-9dae-4c08-9cfb-1a570e4c05bc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Call a Configuration Manager Object Class Method by Using Managed Code
To call a SMS Provider class method, in Configuration Manager, you use the [ExecuteMethod](/previous-versions/system-center/developer/cc146186(v=msdn.10)) method. You populate a [Dictionary](/previous-versions/visualstudio/visual-studio-6.0/aa239680(v=vs.60)) object with the method's parameters, and the return value is an [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) object that contains the result of the method call.  

> [!NOTE]
>  To call a method on an object instance, use the [ExecuteMethod](/previous-versions/system-center/developer/cc146233(v=msdn.10)) method on the [IResultObject](/previous-versions/system-center/developer/cc147376(v=msdn.10)) object instance.  

### To call a Configuration Manager object class method  

1.  Set up a connection to the SMS Provider. For more information, see [SMS Provider fundamentals](sms-provider-fundamentals.md).  

2.  Create the input parameters as a **Dictionary** object.  

3.  Using the **WqlConnectionManager** object instance, call [ExecuteMethod](/previous-versions/system-center/developer/cc146186(v=msdn.10)) and specify the class name and input parameters.  

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
 The Configuration Manager exceptions that can be raised are [SmsConnectionException](/previous-versions/system-center/developer/cc147431(v=msdn.10)) and [SmsQueryException](/previous-versions/system-center/developer/cc147436(v=msdn.10)). These can be caught together with [SmsException](/previous-versions/system-center/developer/cc147433(v=msdn.10)).  

## See Also  
 [Objects overview](configuration-manager-objects-overview.md)
 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md)   
 [How to Create a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-create-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Modify a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)   
 [How to Perform an Asynchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)   
 [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md)   
 [How to Read a Configuration Manager Object by Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md)
